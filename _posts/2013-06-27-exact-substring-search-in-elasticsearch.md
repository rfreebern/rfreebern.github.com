--- 
published: true
title: Exact Substring Searches in ElasticSearch
body_class: post
layout: post
summary: Careful indexing and clever queries can provide arbitrary-length exact substring searches against blobs of text in ElasticSearch without making your index balloon in size.
---

At [Union Street Media](http://usmre.com "Union Street Media"), we recently embraced [ElasticSearch](http://elasticsearch.org) as the backend to provide our web application with fast, powerful real estate property listing search capabilities.

The transition from MySQL to ElasticSearch was a learning experience, as ElasticSearch is far more strict about data types and forces you to think fairly comprehensively from the start about how searches are going to be performed against your data -- a good idea, to be sure, but for an application that wasn't built using ElasticSearch from the ground up, it presents some unique challenges.

## The Problem: Arbitrary-length exact substring search

Our clients and users have a common use-case that wasn't simple to provide in ElasticSearch: the ability to search for arbitrary-length exact substrings of large text blobs. If you're looking for properties where the description (which could be a couple thousand characters long) contains "large yard", you don't want one that says "this large property has no yard", but ElasticSearch's default tokenizer would match this.

Based on the usage patterns in our system, the expectations of our clients, and the need to support tens of thousands of pre-existing searches, finding a way to provide arbitrary exact substring matching was necessary. Searching the web for a way to implement this turned up little, and most of what I could find didn't solve the problem in a way that worked for us, so I set out to solve it on my own.

## First Attempt: Too big, too limited

The obvious starting point for exact substring matches was [ngram tokenizing](http://www.elasticsearch.org/guide/reference/index-modules/analysis/ngram-tokenizer/), which indexes all the substrings up to length *n*. The drawback of ngram tokenizing is the large amount of disk space used. Tokenizing the fields that are used for exact-substring searches in our system for ngrams up to 24 characters long ballooned our index's size on disk from 7 to almost 40GB -- and I hadn't even indexed all the documents I needed at that point. 

To ensure that the search terms were analyzed as a single string, I set up a custom `keyword` search analyzer for the fields. After setting up the index this way, searches were snappy, but any search term over 24 characters long failed, and the size on disk was worrisome.

## Our Solution: A compromise between space and complexity

The solution to both the disk usage problem and the too-long search term problem was to compromise by using more complex queries (which in turn uses slightly more CPU to process). The idea is basically to create ngrams up to a given length (I chose 8 characters) and then, when given a search with more than 8 characters, turn it into a boolean AND query looking for every distinct 8-character substring in that string. For example, if a user searched for "large yard" (a 10-character string), the search would be:

    "large ya" AND "arge yar" AND "rge yard"

While theoretically this could result in incorrect matches (if a document contains those 8-character substrings in different locations, e.g. "*large ya*k b*arge yar*n fo*rge yard*"), in practice we haven't seen significant false positives to give us concern.

## How to do it

Here's an example setup for an index using this technique:

{% highlight javascript %}
{
    "mappings": {
        "homes": {
            "properties": {
                "desc": {
                    "type": "string",
                    "index_analyzer": "index_ngram",
                    "search_analyzer": "search_ngram"
                }
            }
        }
    },
    "settings": {
        "analysis": {
            "filter": {
                "desc_ngram": {
                    "type": "ngram",
                    "min_gram": 3,
                    "max_gram": 8
                }
            },
            "analyzer": {
                "index_ngram": {
                    "type": "custom",
                    "tokenizer": "keyword",
                    "filter": [ "desc_ngram", "lowercase" ]
                },
                "search_ngram": {
                    "type": "custom",
                    "tokenizer": "keyword",
                    "filter": "lowercase"
                }
            }
        }
    }
}
{% endhighlight %}

Put this in a file, say `settings.json`, and then

    curl -s -XPUT 'localhost:9200/listings' -d @settings.json

Add some data:

    curl -s -XPUT 'localhost:9200/listings/homes/1' -d '{ "desc": "This is a lovely home with a large yard." }'
    curl -s -XPUT 'localhost:9200/listings/homes/2' -d '{ "desc": "This large fixer-upper has a gravelly yard." }'
    curl -s -XPUT 'localhost:9200/listings/homes/3' -d '{ "desc": "A colonial mansion with a large yard and a pool." }'

Then, your query for the phrase "large yard" would end up like this:

    curl -s -XGET 'localhost:9200/listings/homes/_search?pretty=true' -d '{ "query" : { "bool" : { "must" : [ { "match" : { "desc" : { "query" : "large ya", "type" : "phrase" } } }, { "match" : { "desc" : { "query" : "arge yar", "type" : "phrase" } } }, { "match" : { "desc" : { "query" : "rge yard", "type" : "phrase" } } } ] } } }'; echo

Which gives the result:

{% highlight javascript %}
{
  "took" : 8,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 2,
    "max_score" : 0.03321779,
    "hits" : [ {
      "_index" : "listings",
      "_type" : "home",
      "_id" : "1",
      "_score" : 0.03321779, "_source" : { "desc" : "This is lovely home with a large yard." }
    }, {
      "_index" : "listings",
      "_type" : "home",
      "_id" : "3",
      "_score" : 0.029065568, "_source" : { "desc" : "A colonial mansion with a large yard and a pool." }
    } ]
  }
}
{% endhighlight %}

The document with ID 2 doesn't appear, because while its `desc` field contains both "large" and "yard", it doesn't contain the exact string "large yard".

Finally, a PHP snippet to build your queries. This code uses [Elastica](http://elastica.io):

{% highlight php %}
function exactSubstringQuery ($field, $value) {
    $substrings = array($value);
    if (strlen($value) > 8) {
        $substrings = array();
        $i = 0;
        while (strlen($chunk = substr($value, $i++, 8)) == 8) {
            $substrings[] = $chunk;
        }
    }
    $boolQuery = new Query\Bool();
    foreach ($substrings as $value) {
        $query = new Query\Match();
        $boolQuery->addMust($query->setField($field)->setFieldQuery($field, $value)->setFieldParam($field, 'type', 'phrase'));
    }
    return $boolQuery;
}
{% endhighlight %}

I don't claim to be an ElasticSearch expert by any means, but this technique solved a problem for us given our constraints. I hope it helps someone else!
