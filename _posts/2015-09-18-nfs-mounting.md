---
layout:     post
title:      Mounting NFS Share
date:       2015-09-18 00:53:29
summary:    Mounting on Centos
categories: viz code data
---

### Mounting NFS Share
This is pretty simple and straightforward, I am just blogging about it to keep it here for reference instead of keep Googling for it. My setup is pretty straight forward. I have an NFS server, three physical servers, and bunch of VMs running on the physical servers. One of my VMs is a web server that hosts content that is produced by backend workers. The data is written to a Riak database and I only need to mount the Riak folder on my VM as read-only. 

First thing to do is install the utilities on Centos:
{% highlight bash %}
sudo yum install nfs-utils nfs-utils-lib
{% endhighlight %}

Then you need to create a directory to mount the share to:
{% highlight bash %}
sudo mkdir -p /myshare/path
{% endhighlight %}

Finally, mount the share:

{% highlight bash %}
sudo mount -t nfs -o ro,nolock 10.20.30.40:/sharename /myshare/pth
{% endhighlight %}

##### Notes
1. This mounts the share as read-only
2. I am using **nolock** option since I will not be writing to the share
3. If you want to write to the share, I recommend you run statd and use locking, otherwise we all will end up speaking Mexican (Ayudame!):

{% highlight bash %}
mount.nfs: rpc.statd is not running but is required for remote locking.
mount.nfs: Either use '-o nolock' to keep locks local, or start statd.
mount.nfs: an incorrect mount option was specified
{% endhighlight %}

If you need locking, you have to install nfs-common package

{% highlight bash %}
sudo yum install nfs-common
{% endhighlight %}

Then you can go ahead and turn on the service and start it:
{% highlight bash %}
sudo chkconfig statd on
sudo service statd start
{% endhighlight %}

4. To make sure the mounts are persistent, configure /etc/fstab

