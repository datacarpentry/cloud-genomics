---
title: "Introuducing FASTQ format and error profiles"
teaching: 0
exercises: 0
questions:
- "Key question"
objectives:
- "First objective."
keypoints:
- "First key point."
---

Approximate time: 

## Learning Objectives:

* Download file from the internet with wget
* Transfer a file from remote machine to your computer with FileZilla
* Transfer a file from your computer to remote machine with FileZilla
* Name other tools that can be used for file transfer

# Download file from the internet to your remote machine

One way to download files to your remote instance from a webserver is to use the command line tool, *wget*. This command supports downloading files from FTP and HTTP(s). The tool *wget* also supports recursive download (with the parameter *-r*), allowing you to download content from a directory or folder. For your information, there are other command line tools that can also be used to download data (e.g., *curl*), but *wget* should serve you well for this lesson and bioinformatic analysis.


```bash
$ wget ftp://bacteria.ensemble....
```

# Move file from remote instance to local machine
If the data is not located on a webserver, *wget* will not work. Instead, you can use FileZilla to transfer a file from you local machine to a remote instance, or vice versa. 

######Filezilla - Step 1

Open *FileZilla*, and click on the File tab. Choose 'Site Manager'.
 
![FileZilla_step1](../img/Filezilla_step1.png) **ADD IMAGE**

######Filezilla - Step 2

Within the 'Site Manager' window, do the following: 

1. Click on 'New Site', and name it something intuitive (e.g. dc or Data_Carpentry)
2. Host: address of your cloud instance (e.g. ec2-...) 
3. Protocol: SFTP - SSH File Transfer Protocol
4. Logon Type: Normal
5. User: dcuser
6. Password: data4Carp
7. Click 'Connect'
	
![FileZilla_step2](../img/FileZilla_step2.png) **ADD IMAGE**

######Filezilla - Step 3

In FileZilla, on the left side of the screen navigate to the location you would like to save the file, and on the right side of the screen navigate through your remote directory to the file **MODIFY FILE NAME** `/home/dcuser/dc_workshop/results/fastqc_untrimmed_reads/SRR097977_fastqc.html`. Double click on the .html file to transfer a copy, or click and drag over to the right hand panel.

Open the file on your local machine.



















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
