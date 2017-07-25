---
layout: page
title: "Instructor Notes"
permalink: /guide/
---
# Cloud Genomics Pre-Workshop 

Using the cloud genomics lesson materials may involve using Amazon EC2 instances. To get this up and running, do the following:

+ Find out how many learners you are expecting. Contact your host for this information. You will likely want to have a couple extra instances lying around in case one dies.
+ Start an etherpad for the workshop.
+ Contact Tracy with the dates of your workshop, a link to the etherpad and the number of learners expected. She will start the instances, and they will appear in your etherpad.

**VM Image Directories**
A high-level listing of the directory tree from the `dcuser` account is shown below. Please note that is may be subject to change over time, but we'll try to remember to update this doc.

```
dcuser@ip-172-31-50-230:~$ tree -L 2
.
├── dc_sample_data
│   ├── r_genomics
│   ├── sra_metadata
│   └── untrimmed_fastq
├── Desktop
│   ├── firefox.desktop
│   ├── gnome-terminal.desktop
│   ├── nautilus.desktop
│   └── rstudio.desktop
├── Downloads
├── FastQC
│   ├── Configuration
│   ├── fastqc
│   ├── fastqc_icon.ico
│   ├── Help
│   ├── INSTALL.txt
│   ├── jbzip2-0.9.jar
│   ├── LICENSE.txt
│   ├── net
│   ├── org
│   ├── README.txt
│   ├── RELEASE_NOTES.txt
│   ├── run_fastqc.bat
│   ├── sam-1.103.jar
│   ├── Templates
│   └── uk
├── openrefine-2.6-beta.1
│   ├── licenses
│   ├── LICENSE.txt
│   ├── README.txt
│   ├── refine
│   ├── refine.ini
│   ├── server
│   └── webapp
├── R
│   └── x86_64-pc-linux-gnu-library
└── Trimmomatic-0.32
    ├── adapters
    ├── LICENSE
    └── trimmomatic-0.32.jar

21 directories, 19 files
```

# During the workshop

We had a couple instances die as we were going through our workshop.

+ First, check that this isn't an issue with the student's network settings. Try and load a different website to verify that their internet is working.
+ Try to connect to the instance on a different machine, or with a different protocol. For instance, if the student is working in PuTTy, try to connect using scp.
+ Try to ping the instance like so:

```UNIX
ping hostname
```

+ If the student's internet is working, you can't connect via a different protocol or you can't ping the instance, probably it's died. Assign the student to a new instance. We had 2 out of ~30 die at our workshop at ISU.
