---
title: "Data roundtripping"
teaching: 15
exercises: 5
questions:
- How do I move data into the cloud?
- How do I get my analysis results back to my computer?
objectives:
- Transfer data into a cloud session
- Transfer data out of a cloud session
keypoints:
- No matter which way you want to move data, it's easier to start the transfer from your local machine
---

<script language="javascript" type="text/javascript">
function set_page_view_defaults() {
    document.getElementById('div_aws_win').style.display = 'block';
    document.getElementById('div_aws_unix').style.display = 'none';
};

function change_content_by_platform(form_control){
    if (!form_control || document.getElementById(form_control).value == 'aws_win') {
        set_page_view_defaults();
    } else if (document.getElementById(form_control).value == 'aws_unix') {
        document.getElementById('div_aws_win').style.display = 'none';
        document.getElementById('div_aws_unix').style.display = 'block';
    } else {
        alert("Error: Missing platform value for 'change_content_by_platform()' script!");
    }
}

window.onload = set_page_view_defaults;
</script>


## Moving data is simple
(but not always easy!)

Now that you're on the cloud, you'll need data. There are two main places you can get data
from: your local machine, or other machines in the cloud, like NCBI.

How you get your data depends on where the data is right now.

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

```
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

```
    cd
    wget ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt
```
or

```
    cd
    curl -O ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt
```

Since we wanted to *download* the file rather than just view it, we used ``wget`` without
any modifiers. With ``curl`` however, we had to use the -O flag, which simultaneously tells ``curl`` to
download the page instead of showing it to us **and** specifies that it should save the
file using the same name it had on the server: species_EnsemblBacteria.txt

It's important to note that both ``curl`` and ``wget`` download to the computer that the
command line belongs to. So, if you are logged into AWS on the command line and execute
the ``curl`` command above in the AWS terminal, the file will be downloaded to your AWS
machine, not your local one.

### Moving files between your laptop and your instance

What if the data you need is on your local computer, but you need to get it *into* the
cloud? There are also several ways to do this, but it's *always* easier
to start the transfer locally. **This means if you're using a transfer program, it needs to be
installed on your local machine, not on your instance. If you're typing into a terminal,
the terminal should not be logged into your instance, it should be showing your local computer.**

These directions are platform specific so please follow the instructions for your system:

**Please select the platform you wish to use for the exercises: <select id="id_platform" name="platformlist" onchange="change_content_by_platform('id_platform');return false;"><option value="aws_unix" id="id_aws_unix" selected> AWS_UNIX </option><option value="aws_win" id="id_aws_win" selected> AWS_Windows </option></select>**


<div id="div_aws_win" style="display:block" markdown="1">


### Uploading Data to your Virtual Machine

If you're using a PC, we recommend you use the *PSCP* program. This program is from the same suite of
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
5. Locate a file on your computer that you wish to upload (be sure you know the path). Then upload it to your remote machine (**you will need to know your ip address, and login credentials**). You will be prompted to enter a password, and then your upload will begin. **(make sure you use substitute 'your-pc-username' for your actual pc username)**

   ```
C:\User\your-pc-username\Downloads> pscp.exe local_file.txt dcuser@ip.address:/home/dcuser/
```

### Downloading Data from your Virtual Machine

1. Follow the instructions in the Upload section to download (if needed) and access the *PSCP* program (steps 1-3)
2. Download the zipped fastqc report using the following command **(make sure you use substitute 'your-pc-username' for your actual pc username and dcuser@ ip.address with your remote login credentials)**

```
C:\User\your-pc-username\Downloads> pscp.exe dcuser@ip.address:/home/dcuser/dc_workshop/results/fastqc_untrimmed_reads/SRR097977_fastqc.zip C:\User\your-pc-username\Downloads
```

</div>



<div id="div_aws_unix" style="display:block" markdown="1">

`scp` stands for 'secure copy protocol', and is a widely used UNIX tool for moving files
between computers. The simplest way to use `scp` is to run it in your local terminal,
and use it to copy a single file:

```
scp <file I want to move> <where I want to move it>
```

Note that you are always running `scp` locally, but that *doesn't* mean that
you can only move files from your local computer. A command like:

```
scp <local file> <AWS instance>
```

To move it back, you just re-order the to and from fields:

```
scp <AWS instance> <local file>
```

### Uploading Data to your Virtual Machine

1. Open the terminal and use the `scp` command to upload a file (e.g. local_file.txt) to the dcuser home directory:

```bash
$  scp local_file.txt dcuser@ip.address:/home/dcuser/
```

### Downloading Data from your Virtual Machine

Let's download a zipped file from our remote machine.  You should have a fastqc report in ~/dc_workshop/results/fastqc_untrimmed_reads/SRR097977_fastqc.zip

**Tip:** If you are looking for another (or any really) zip file in your home directory to use instead try

```bash
$ find ~ -name *.zip
```


1. Download the fastqc report in ~/dc_workshop/results/fastqc_untrimmed_reads/SRR097977_fastqc.zip to your home ~/Dowload directory using the following command **(make sure you use substitute dcuser@ ip.address with your remote login credentials)**:

   ```bash
$ scp dcuser@ip.address:/home/dcuser/dc_workshop/results/fastqc_untrimmed_reads/SRR097977_fastqc.zip ~/Downloads
```

Remember that in both instances, the command is run from your local machine, we've just flipped the order of the to and from parts of the command.
</div>
