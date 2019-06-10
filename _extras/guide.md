---
layout: page
title: "Instructor Notes"
---
# Cloud Genomics Pre-Workshop 

The cloud genomics lesson materials are intended to be used late in the workshop, after the learners are comfortable with the command line and concepts. There is limited computation, however it does require some use of the Amazon EC2 instances. It is designed to give learners a chance to think about how they will do computation on their own after the workshop, and to ask questions about how to access and choose among computing resources.

# Log In issues

If instances die during the workshop:

+ First, check that this isn't an issue with the student's network settings. Try and load a different website to verify that their internet is working.
+ Try to connect to the instance on a different machine, or with a different protocol. For instance, if the student is working in PuTTy, try to connect using scp.
+ Try to ping the instance like so:

```UNIX
ping hostname
```

+ If the student's internet is working, you can't connect via a different protocol or you can't ping the instance, the instance itself is probably the problem. The fastest solution is to assign the student to a new instance that isn't being used. Typically, you'll have a handful of 'extra' instances spun up for your workshop for just this situation.

# Discussion of computing resources

We've provided some background info on several common computing resources (AWS, HPCs, XSEDE) and are always adding more. At minimum, we've provided links out to information on other services. It helps to skim over these before your workshop to familarize yourself, but no one expects you to be an expert on all of these. In most instances you can answer learner questions just by screensharing the lesson page and clicking through the links we've provided. 
