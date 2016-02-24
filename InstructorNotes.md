#Cloud Genomics Pre-Workshop 

Using the cloud genomics lesson materials involves using Amazon EC2 instances. To get this up and running, do the following:

+ Find out how many learners you are expecting. Contact your host for this information. You will likely want to have a couple extra instances lying around in case one dies.
+ Start an etherpad for the workshop.
+ Contact Tracy with the dates of your workshop, a link to the etherpad and the number of learners expected. She will start the instances, and they will appear in your etherpad.

#During the workshop

We had a couple instances die as we were going through our workshop.

+ First, check that this isn't an issue with the student's network settings. Try and load a different website to verify that their internet is working.
+ Try to connect to the instance on a different machine, or with a different protocol. For instance, if the student is working in PuTTy, try to connect using scp.
+ Try to ping the instance like so:

```UNIX
ping hostname
```

+ If the student's internet is working, you can't connect via a different protocol or you can't ping the instance, probably it's died. Assign the student to a new instance. We had 2 out of ~30 die at our workshop at ISU.