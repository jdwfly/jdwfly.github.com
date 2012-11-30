---
layout: post
title: Rackspace Cloudfiles Python API getURLs
published: true
---

So it ended up one day that I needed to grab a lot of URL addresses from files we have on [Rackspace Cloudfiles](http://www.rackspace.com/cloud/public/files/). If you have never used their builtin interface then you have saved yourself from getting a headache. The good news is that they have released an [API](http://www.rackspace.com/cloud/public/files/api/). So with just a few lines of python code I am up and running with a script that grabs all the URL addresses out of a single container. Hopefully this might help someone get up and running with their API.  

First of all if you have not downloaded their Cloudfiles API head over to their [Github repo](https://github.com/rackspace/python-cloudfiles) to download and install.  

<script src="https://gist.github.com/4172792.js?file=getURLs.py"> </script>  

Obviously you will need to change the three variables to whatever is appropiate for you. If you want to do something more than this check out their [documentation](http://packages.python.org/python-cloudfiles/cloudfiles-module.html).