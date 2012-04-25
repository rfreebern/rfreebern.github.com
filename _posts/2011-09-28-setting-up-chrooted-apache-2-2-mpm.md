--- 
published: true
title: Setting up chrooted Apache 2.2 MPM
body_class: post
layout: post
---




Some stumbling blocks I ran into while setting up a chrooted Apache 2.2.14 on Ubuntu 10.04.

*   Apache 2.2.10 and later have chroot capability built-in, so there's no need to install mod_chroot.
*   Once you've set the server-wide `ChrootDir` directive and updated your vhost `DocumentRoot`s to be relative to it, the various server start commands (`apachectl start`, `service apache2 start`, etc.) may complain that your `DocumentRoot` doesn't exist. This is because it's not chrooted yet and it's looking for the directories relative to the filesystem root instead of relative to your `ChrootDir`. You can ignore this.
*   If your error log fills up with:
        
        [Tue Sep 27 22:06:13 2011] [notice] child pid 11436 exit signal Aborted (6)
        libgcc_s.so.1 must be installed for pthread_cancel to work
    
    it means you need to add the line 
        
        LoadFile /lib/libgcc_s.so.1 to your server configuration.

I hope someone else finds this helpful!
