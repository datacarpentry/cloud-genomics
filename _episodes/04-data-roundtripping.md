---
title: "Data roundtripping"
teaching: 15
exercises: 5
questions:
objectives:
- "First objective."
keypoints:
- "First key point."
---

# Data Roundtripping

# Learning Objectives
* Describe the need to employ file transfer tools
* Identify options for moving files between a computer and a cloud session.
* Upload data to a virtual machine (cloud session).
* Download data from a virtual machine (cloud session).

## Moving data is simple
(but not always easy!)

Now that you're on the cloud, you'll need data. There are two main places you can get data
from: your local machine, or other machines in the cloud, like NCBI.

How you get your data, depends on where the data is right now. 

### Getting data from the cloud

There are two programs that will download data from a remote server to your local 
(or remote) machine: ``wget`` and ``curl``. They were designed to do slightly different 
tasks by default, so you'll need to give the programs somewhat different options to get
the same behaviour, but they are mostly interchangeable.

 - ``wget`` is short for "world wide web get", and it's basic function is to *download* 
 web pages or data at a web address.

 - ``cURL`` is a pun, it is suppose to be read as "see URL", so it's basic function is 
 to *display* webpages or data at a web address.

Which one you need to use mostly depends on your operating system, as most computers will 
only have one or the other installed by default.

Let's say you want to download some data from Ensembl. We're going to download a very small
tab-delimited file that just tells us what data is available on the Ensembl bacteria server.
Before we can start our download, we need to know whether we're using ``curl`` or ``wget``. 

#### Exercise

To see which program you have:

```bash
    which curl
    which wget
```

``which`` is a BASH program that looks through everything you have
installed, and tells you what folder it is installed to. If it can't
find the program you asked for, it returns nothing, i.e. gives you no
results.

On OSX, you'll likely get:

```bash
    $ which curl
    /usr/bin/curl
    $ which wget
    $ 
```

Once you know whether you have ``curl`` or ``wget`` use one of the
following commands to download the file:

.. code:: bash

    cd
    wget ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt

or

.. code:: bash

    cd
    curl -O ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt

Since we wanted to *download* the file rather than just view it, we used ``wget`` without
any modifiers. With ``curl`` however, we had to use the -O flag, which tells ``curl`` to
download the page instead of showing it to us **and** specifies that it should save the 
file using the same name it had on the server: species_EnsemblBacteria.txt

It's important to note that both ``curl`` and ``wget`` download to the computer that the
command line belongs to. So, if you are logged into AWS on the command line and execute 
the ``curl`` command above in the AWS terminal, the file will be downloaded to your AWS 
machine, not your local one.

### Moving files between your laptop and your instance

What if the data you need is on your local computer, but you need to get it *into* the 
cloud? There are also several ways to do this. These directions are platform specific so
please follow the instructions for your system

## Uploading Data to your Virtual Machine

#### PC

Using PC, we recommend you use the *PSCP* program. This program is from the same suite of 
tools as the putty program we have been using to connect. 

1. If you haven't done so, download pscp from [http://the.earth.li/~sgtatham/putty/latest/x86/pscp.exe](http://the.earth.li/~sgtatham/putty/latest/x86/pscp.exe)
2. Make sure the *PSCP* program is somewhere you know on your computer. In this case,
your Downloads folder is appropriate. 
3. Open the windows [PowerShell](https://en.wikipedia.org/wiki/Windows_PowerShell); 
go to your start menu/search enter the term **'cmd'**; you will be able to start the shell
(the shell should start from C:\Users\your-pc-username>). 
4. Change to the download directory

```
> cd Downloads
```
5. locate a file on your computer that you wish to upload (be sure you know the path). Then upload it to your remote machine (**you will need to know your ip address, and login credentials**). You will be prompted to enter a password, and then your upload will begin. **(make sure you use substitute 'your-pc-username' for your actual pc username)**

   ```
C:\User\your-pc-username\Downloads> pscp.exe local_file.txt dcuser@ip.address:/home/dcuser/
```

#### MAC/Linux

1. Open the terminal and use the *scp* command to upload a file (e.g. local_file.txt) to the dcuser home directory:

   ```bash
$  scp local_file.txt dcuser@ip.address:/home/dcuser/
```
## Downloading Data from your Virtual Machine

Let's download a zipped file from our remote machine.  You should have a fastqc report in ~/dc_workshop/results/fastqc_untrimmed_reads/SRR097977_fastqc.zip

**Tip:** If you are looking for another (or any really) zip file in your home directory to use instead try

```bash
$ find ~ -name *.zip
```

#### PC

1. Follow the instructions in the Upload section to download (if needed) and access the *PSCP* program (steps 1-3)
2. Download the zipped fastqc report using the following command **(make sure you use substitute 'your-pc-username' for your actual pc username and dcuser@ ip.address with your remote login credentials)**

```
C:\User\your-pc-username\Downloads> pscp.exe dcuser@ip.address:/home/dcuser/dc_workshop/results/fastqc_untrimmed_reads/SRR097977_fastqc.zip C:\User\your-pc-username\Downloads
```
#### Mac/Linux

1. Download the fastqc report in ~/dc_workshop/results/fastqc_untrimmed_reads/SRR097977_fastqc.zip to your home ~/Dowload directory using the following command **(make sure you use substitute dcuser@ ip.address with your remote login credentials)**:

   ```bash
$ scp dcuser@ip.address:/home/dcuser/dc_workshop/results/fastqc_untrimmed_reads/SRR097977_fastqc.zip ~/Downloads
```

## Moving data to your iPlant (or iRODS) Account

If you have an iPlant account, or storage on an iRods server, we can you iCommands to move the data to your personal Data Store. 

If you are unfamiliar with iCommands see their [documentation](https://docs.irods.org/master/icommands/user/)

### Setting up iCommands for iPlant

1. Initialize iCommands using the following command

   ```bash
$ iinit
```
2. You will then be asked to setup your account and will need to enter the following information

   |Prompt|Entry|
|------|-----|
|irodsHost|data.iplantcollaborative.org|
|port|1247|
|zone|iplant|
|irodsUserName|your iplant username|
|Current iRODS password|your iplant password|
3. Verify that you have connected to your iPlant Data Store; view the contents of your home directory using the following the *ils* command:

   ```bash
$ ils
```

#### Moving Data to and from your remote machine to Data Store

##### Move to Data Store
To move data from a local source to iPlant use the *iput* command. In this case we pass the -P option to see the progress of the transfer. 

```
$ iput -P remote_machine_file.txt .
```
**Tip:** in this case, the '.' stands for the current iPlant working directory which is by default '/iplant/home/your-iplant-username'

#### Retrieve from Data Store

Use the *iget* command to move files from the Data Store into your remote machine:

```
$ iget -P iplant_datastore_file.txt .
```

There are several other iCommands options (including how to use the -T option for more reliable big data transfers, and -r command for recursive transfers of directories - See [iCommands documentation](https://pods.iplantcollaborative.org/wiki/display/DS/Using+iCommands). 
