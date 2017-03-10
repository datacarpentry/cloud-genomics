---
title: "Moving Data"
teaching: 0
exercises: 0
questions:
- "Key question"
objectives:
- "First objective."
keypoints:
- "First key point."
---

# Move data onto your instance

## Surprise!

You've already been working on the cloud instance and moving data from external servers onto your instance as well as moving data around your instance.

Remember, when you downloaded the *E. coli* dataset to work with?

    wget ftp://blahblahblahblah

In this case, you are using a command line tool, *wget*, to download content from a webserver.  This command supports downloading files from FTP and HTTP(s).  The tool *wget* also supports recursive download (with the parameter *-r*), allowing you to download content from a directory or folder.  For your information, there are other command line tools that can also be used to download data (e.g., *curl*), but *wget* should serve you well for this lesson and bioinformatic analysis.

## Moving files between your laptop and your instance

If you're interested in transferring files on your computer to your instance, you can follow these operating-specific [instructions](http://angus.readthedocs.org/en/2014/amazon/transfer-files-between-instance.html).