---
title: "Which Cloud for my data?"
teaching: 10
exercises: 20
questions:
- What cloud resources are available?
- How do I choose my resources?
objectives:
- Describe the advantages and disadvantages of various cloud computing platforms.
- Determine what resources a project will require
- Match required resources to computing platforms
---


## Cloud platform choices

There are several cloud providers to choose from. Some scientific clouds may either be free or allocate resources competitively. Commercial clouds can be very powerful, but choice can be overwhelming. We will cover as much as we can, but you will ultimately need to learn things not covered here so see the documentation below:

The major tradeoff between platforms is between flexibility and cost. Generally speaking,
services that allow you more flexibility and autonomy will be more expensive than
highly managed services.

### University/Corporate Computing Clusters

Many universities and businesses operate their own computing clusters that are available to students and staff
at low or no cost. If your employer maintains a computing cluster, this will almost always be the least
expensive option.

However, most HPCCs (High Performance Computing Clusters) put limits on:
 - the number of processors a user can utilize at once
 - the amount of disk storage per user
 - the amount of time a single process can run
 - what programs can be installed, and by whom
 - who can have accounts and access data

 HPCCs are also a shared resource, so even when you have access, your programs are unlikely to run
 immediately. Most HPCCs run some kind of scheduler, that you submit your processing jobs to, and
 it runs them as resources become available. In order to submit a job, you generally will need to
 know not only what program you want to run, but with how many processors and for how long.
 While interacting with the scheduler is no more difficult than interacting with the shell,
 it will have its own set of commands and syntax that you'll need to learn; and these vary
 widely among HPCCs.

 There are also many upsides to using an HPCC. As previously mentioned, they're generally the least
 expensive option, but they often come with more perks. For instance, many HPCCs offer free or low-cost
 training, storage space, back-up options, and technical support. If your HPCC has a scheduler, you
 can also queue up many sequential jobs all at once, and you don't have to worry about racking up
 fees on instances that are sitting idle. It's often also much easier to pay for HPCC use than to
 pay for Amazon using grant money, however universities are getting better about AWS payments.

### Public Computing Clusters

#### [XSEDE](https://www.xsede.org/)


### Commercial Clouds

#### [Amazon EC2 ](http://aws.amazon.com/ec2/)

[Amazon Web Services](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)

#### [Google Cloud](https://cloud.google.com/)

[Google Cloud](https://cloud.google.com/compute/docs/quickstart)

#### [Microsoft Azure](https://azure.microsoft.com/en-us/)


### Open Science Clouds

#### [Atmosphere](https://pods.iplantcollaborative.org/wiki/display/atmman/Getting+Started)


#### [CyVerse (iPlant Collaborative) Atmosphere](http://www.cyverse.org/atmosphere)


#### [JetStream](http://jetstream-cloud.org/)


## Exercise

In small groups or on your own, plot out your next bioinformatics project. With guidance
from your instructors and the above references, try to determine not only what types of
resources you'll need, but what platform will best suit your project.

Some things to consider:

- How much data do you have?
- What computational steps will it need?
  - What is the *largest* computational step?
  - Can any steps be done in parallel?
- What is your timeframe?
- Who will be doing most of the computational work?
  - What computational skills do they have?
  - Do you need to share the data across many labs?
- How many times will you need to run this pipeline?



### Other Resources:


Learn more about cloud computing in bioinformatics<br>
Fusaro VA, Patil P, Gafni E, Wall DP, Tonellato PJ (2011) **Biomedical Cloud Computing With Amazon Web Services**. PLoS Comput Biol 7(8): e1002147. doi: 10.1371/journal.pcbi.1002147
