---
title: "Logging onto Cloud"
teaching: 5
exercises: 5
questions:
- How do I connect to an AWS instance?
objectives:
- Connect to a running instance
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
        document.getElementById('div_hpc').style.display = 'none';
        document.getElementById('div_cyverse').style.display = 'none';
    } else {
        alert("Error: Missing platform value for 'change_content_by_platform()' script!");
    }
}

window.onload = set_page_view_defaults;
</script>

## Important Note

This lesson covers how to log into, and out of, an *already running* Amazon instance.

If you're returning post-workshop and want to launch your own instance, use [launching cloud instances on your own](../discuss/)

## Background to AWS

Setting up a new AWS instance requires a credit card, an AWS account, and up to
a day of verification time, but you've already spent most of this workshop working in the cloud!
To save time, your instructor launched a remote computer (instance) for you prior
to the workshop, and connected it to our lesson data. You've already logged into it at
least once, but now that you're more comfortable with the command line, lets go back and talk about how it all works.


We have a pre-configured copy of the data needed for this workshop that is always available
to attach to a new instance on Amazon, as long as you have an account, and the log-in credentials to open it.

To access the pre-configured workshop data, you'll need to use our log-in credentials;
that is, you need our user name and password:

**Log-in Credentials**
Credentials are case sensitive:

- Username: dcuser
- Password: data4Carp

But first, you need a place to log *into*! To find the instance that's attached to that data,
you'll need something called an IP address. Your instructor should have given this to you
at the beginning of the workshop.

An IP address is essentially the numerical version of a web address like www.amazon.com

Recall that cloud computing is about choice. You can rent just a single processor on a large computer
for a small project, or you can rent hundreds of processors spread across multiple computers for
a large project. In either case, once you rent the collection of processors, Amazon will
present your rental to you as if it was a single computer. So, the physical computers that host your
instances don't really move, *but* every time you launch a new instance, it will have a new IP address.

So, each time you launch a new instance, the *IP address* changes, but your *Log-in Credentials* don't have to.

## Connection Protocols

We will use a protocol called Secure Shell (SSH) that, as the name implies, provides you
with a secure way to use a [shell](http://swcarpentry.github.io/shell-novice). In our case,
the shell will be running on a remote machine. This protocol is available for every
operating system, but sometimes requires additional software.

## Logging onto a cloud instance

**Please select the platform you wish to use for the exercises: <select id="id_platform" name="platformlist" onchange="change_content_by_platform('id_platform');return false;"><option value="aws_unix" id="id_aws_unix" selected> AWS_UNIX </option><option value="aws_win" id="id_aws_win" selected> AWS_Windows </select>**


<div id="div_aws_win" style="display:block" markdown="1">

## Exercises<br>

#### **Connecting using PC**<br>
*Prerequisites*: You must have an SSH client. There are several free options but you should have installed [[PuTTY.exe](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)] at the begining of the workshop, and we're going to continue using that.<br>


1. Open PuTTY; In the 'Host Name (or IP address)' section paste in the IP address provided by your instructor (or the ip address of an instance you have provisioned yourself). *Keep the default selection 'SSH' and Port (22)*. <br>
<p><img src="../fig/putty_screenshot_1.png" width="500"></p>
2. Click 'Open' and you will be presented with a security warning. Select 'Yes' to continue to connect. <br>
<p><img src="../fig/putty_screenshot_2.png" width="500"></p>
3. In the final step, you will be asked to provide a login and password. **Note:** When typing your password, it is common in Unix/Linux not see see any asterisks (e.g. ****) or moving cursors. Just continue typing.<br>
<p><img src="../fig/putty_screenshot_3.png" width="500"></p>
4. You should now be connected!

</div>




<div id="div_aws_unix" style="display:block" markdown="1">


#### **Connecting using Mac/Linux**<br>
*Prerequisites*: Mac and Linux operating systems will already have terminals installed. Simply search for 'Terminal' and/or look for the terminal icon.<br>
![terminal icon](../fig/terminal.png)<br>


1. Open the terminal and type the following command substituting 'ip_address' for the ip address your instructor will provide (or the ip address of an instance you have provisioned yourself). *Be sure to pay attention to capitalization and spaces*<br>

```bash
        $ ssh dcuser@ip_address
```
<br>
2. You will receive a security message that looks something like the message below. Type 'yes' to proceed.<br>

```bash
        The authenticity of host 'ec2-52-91-14-206.compute-1.amazonaws.com (52.91.14.206)' can't be established.
        ECDSA key fingerprint is SHA256:S2mMV8mCThjJHm0sUmK2iOE5DBqs8HiJr6pL3x/XxkI.
        Are you sure you want to continue connecting (yes/no)?
```
<br>
3. In the final step, you will be asked to provide a login and password. **Note:** When typing your password, it is common in Unix/Linux not see any asterisks (e.g. ****) or moving cursors. Just continue typing.<br>
4. You should now be connected!

</div>
