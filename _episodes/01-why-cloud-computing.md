---
title: "Why of cloud computing"
teaching: 5
exercises: 0
questions:
- What is cloud computing?
- How do I log into a remote server?
objectives:
- Understand benefits of working on a remote computer system
- Determine what resources a project will require
---

There are a number of reasons why accessing a remote machine is invaluable to any scientists working with large datasets. In the early history of computing, working on a remote machine was standard practice - computers were bulky and expensive. Today we work on laptops or desktops that are more powerful than the sum of the world's computing capacity 20 years ago, but many analyses (especially in genomics) are too large to run on these laptops/desktops and require larger machines, often several of them, where remote access is the only practical solution.

In recent years computational power became a commodity and entire companies were built around a business model that allows you to "rent" computers for as long as you require, at relatively low cost. This is the basic principle behind the **cloud**. You define your computational requirements and off you go.

You'll know you need to start working on the cloud when...

- Your computer does not have enough resources to run the desired analysis (memory, processors, disk space, network bandwidth).
- Your computer is taking hours or days to get through an analysis.
- You cannot install software on your computer (application does not have support for your operating system, conflicts with other existing applications, etc.)
- You cannot afford the infrastructure (hardware, bandwidth, power supply) required to acquire and maintain sufficiently large computers for your analysis.

The cloud is a part of our everyday life (e.g. using Amazon, Google, Netflix, or an ATM involves remote computing). The topic is fascinating but this lesson says '5 minutes or less' so let's get connected. 


### Choosing a cloud platform

The most important thing about *The Cloud* is choice - instead of purchasing a physical computer, you can obtain on-demand computing at almost any scale. This power comes with advantages and disadvantages:

**Advantages of Cloud Computing**

* Access large amounts of computing power on demand
* Full administrative rights - install anything
* Use pre-con../figured images (software already installed)
 

**Disadvantages of Cloud Computing**

* Cloud computing costs money (you must keep track of your costs)
* If you need help, you may not have a local system administrator 
* Images may be poorly documented (you may not be clear on what is installed, or how to use it)
* Form of payment (credit card)*
* Understanding of Amazon's billing and payment (See: [Getting started with AWS Billing and Cost Management](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-getting-started.html))

\* You can use some of Amazon Web Services for free, or see if you qualify for an AWS Grant (See: [https://aws.amazon.com/grants/](https://aws.amazon.com/grants/) ) if you are using AWS for education. The free level of service *will not* be sufficient for working with the amount of data we are using for our lessons. 


### Cloud platform choices

There are several cloud providers to choose from. Some scientific clouds may either be free or allocate resources competitively. Commercial clouds can be very powerful, but choice can be overwhelming. We will cover as much as we you need to get through the Data Carpentry lessons, but you will ultimately need to learn things not covered here so see the documentation below:

#### Commercial Clouds

* [Amazon Web Services](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)
* [Google Cloud](https://cloud.google.com/compute/docs/quickstart)

#### Open Science Clouds
* [Atmosphere](https://pods.iplantcollaborative.org/wiki/display/atmman/Getting+Started)
* [JetStream](http://jetstream-cloud.org/)



### Resources:

Cloud computing offerings:

* Amazon EC2: [http://aws.amazon.com/ec2/](http://aws.amazon.com/ec2/)
* Microsoft Azure: [https://azure.microsoft.com/en-us/](https://azure.microsoft.com/en-us/)
* Google Cloud Platform: [https://cloud.google.com/](https://cloud.google.com/)
* CyVerse (iPlant Collaborative) Atmosphere: [http://www.cyverse.org/atmosphere](http://www.cyverse.org/atmosphere)

Learn more about cloud computing in bioinformatics<br>
Fusaro VA, Patil P, Gafni E, Wall DP, Tonellato PJ (2011) **Biomedical Cloud Computing With Amazon Web Services**. PLoS Comput Biol 7(8): e1002147. doi: 10.1371/journal.pcbi.1002147 


