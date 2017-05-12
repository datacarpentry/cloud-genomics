---
title: "Data roundtripping"
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

# Learning Objectives
* Describe the need to employ file transfer tools
* Identify options for moving files between a computer and a cloud session.
* Upload data to a virtual machine (cloud session).
* Download data from a virtual machine (cloud session).

## Moving data is simple
(but not always easy!)


You've already been working on the cloud instance and moving data from external servers onto your instance as well as moving data around your instance.

Remember, when you downloaded the *E. coli* reference genome 

```bash
$ wget ftp://bacteria.ensemble....
```

In this case, you are using a command line tool, *wget*, to download content from a webserver.  This command supports downloading files from FTP and HTTP(s).  The tool *wget* also supports recursive download (with the parameter *-r*), allowing you to download content from a directory or folder.  For your information, there are other command line tools that can also be used to download data (e.g., *curl*), but *wget* should serve you well for this lesson and bioinformatic analysis.

##Exercises 

### Moving files between your laptop and your instance

These directions are platform specific so please follow the instructions for your system

##Uploading Data to your Virtual Machine

#### PC

Using PC, we recommend you use the *PSCP* program. This program is from the same suite of tools as the putty program we have been using to connect. 

1. If you haven't done so, download pscp from [http://the.earth.li/~sgtatham/putty/latest/x86/pscp.exe](http://the.earth.li/~sgtatham/putty/latest/x86/pscp.exe)
2. Make sure the *PSCP* program is somewhere you know on your computer. In this case, your Downloads folder is appropriate. 
3. Open the windows [PowerShell](https://en.wikipedia.org/wiki/Windows_PowerShell); go to your start menu/search enter the term **'cmd'**; you will be able to start the shell (the shell should start from C:\Users\your-pc-username>). 
4.Change to the download directory
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
##Downloading Data from your Virtual Machine

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
