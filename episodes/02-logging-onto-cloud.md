---
title: "Logging onto Cloud"
teaching: 0
exercises: 0
questions:
- "Key question"
objectives:
- "First objective."
keypoints:
- "First key point."
---
<script language="javascript" type="text/javascript">
function set_page_view_defaults() {
    document.getElementById('div_aws_win').style.display = 'block';
    document.getElementById('div_aws_unix').style.display = 'none';
    document.getElementById('div_cyverse').style.display = 'none';
    document.getElementById('div_hpc').style.display = 'none';
};

function change_content_by_platform(form_control){
    if (!form_control || document.getElementById(form_control).value == 'aws_win') {
        set_page_view_defaults();
    } else if (document.getElementById(form_control).value == 'aws_unix') {
        document.getElementById('div_aws_win').style.display = 'none';
        document.getElementById('div_aws_unix').style.display = 'block';
        document.getElementById('div_hpc').style.display = 'none';
        document.getElementById('div_cyverse').style.display = 'none';
    } else if (document.getElementById(form_control).value == 'cyverse') {
        document.getElementById('div_aws_unix').style.display = 'none';
        document.getElementById('div_cyverse').style.display = 'block';
        document.getElementById('div_hpc').style.display = 'none';
        document.getElementById('div_aws_win').style.display = 'none';
    } else if (document.getElementById(form_control).value == 'hpc') {
        document.getElementById('div_aws_unix').style.display = 'none';
        document.getElementById('div_cyverse').style.display = 'none';
        document.getElementById('div_hpc').style.display = 'block';
        document.getElementById('div_aws_win').style.display = 'none';
    } else {
        alert("Error: Missing platform value for 'change_content_by_platform()' script!");
    }
}

window.onload = set_page_view_defaults;
</script>

## Launching and logging onto a cloud instance

**Please select the platform you wish to use for the exercises: <select id="id_platform" name="platformlist" onchange="change_content_by_platform('id_platform');return false;"><option value="aws_unix" id="id_aws_unix" selected> AWS_UNIX </option><option value="aws_win" id="id_aws_win" selected> AWS_Windows </option><option value="cyverse" id="id_cyverse"> CyVerse </option><option value="hpc" id="id_hpc"> HPC/HTC cluster </option></select>**

# Learning Objectives:

* Describe the advantages and disadvantages of various cloud computing platforms.
* Transfer data into a cloud session using iCommands.
* Terminate a cloud session.

To save time, your instructor will have launched a remote computer (instance) for you prior 
to the workshop. If you are following these lessons on your own, or after the workshop see 
the lesson on [launching cloud instances on your own](../discuss/) for instructions 
on how to do this yourself. 

## Exercises

### **A. Connecting to a remote machine via SSH**

We will use a protocol called Secure Shell (SSH) that, as the name implies, provides you 
with a secure way to use a [shell](http://swcarpentry.github.io/shell-novice). In our case, 
the shell will be running on a remote machine. This protocol is available in several 
software for every operating system. This is the first and last place in these lessons 
where it will matter if you are using PC, Mac, or Linux. After we connect using SSH, 
we will all be on the same operating system/computing environment. 

<div id="div_aws_win" style="display:block" markdown="1">

To save time, your instructor will have launched a remote computer (instance) for you prior 
to the workshop. If you are following these lessons on your own, or after the workshop see 
the lesson on [launching cloud instances on your own](../discuss/) for instructions 
on how to do this yourself. 

**User Credentials**
Credentials are case sensitive:

- Username: dcuser
- Password: data4Carp


#### **Connecting using PC**<br>
*Prerequisites*: You must have an SSH client. There are several free options and we will use PuTTY [[Download Putty.exe](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)]
**(RMF)THIS NEEDS TO GO INTO INSTALLATION INSTRUCTIONS**

1. Open PuTTY; In the 'Host Name (or IP address)' section paste in the IP address provided by your instructor (or the ip address of an instance you have provisioned yourself). *Keep the default selection 'SSH' and Port (22)*. <br>
<p><img src="../fig/putty_screenshot_1.png" width="500"></p>
2. Click 'Open' and you will be presented with a security warning. Select 'Yes' to continue to connect. <br>
<p><img src="../fig/putty_screenshot_2.png" width="500"></p>
3. In the final step, you will be asked to provide a login and password. **Note:** When typing your password, it is common in Unix/Linux not see see any asterisks (e.g. ****) or moving cursors. Just continue typing.<br> 
<p><img src="../fig/putty_screenshot_3.png" width="500"></p>
4. You should now be connected!

</div>




<div id="div_aws_unix" style="display:block" markdown="1">

To save time, your instructor will have launched a remote computer (instance) for you prior to the workshop. If you are following these lessons on your own, or after the workshop see the lesson on [launching cloud instances on your own](../discuss/) for instructions on how to do this yourself. 

**User Credentials**
Credentials are case sensitive:

- Username: dcuser
- Password: data4Carp


#### **Connecting using Mac/Linux**<br>
*Prerequisites*: Mac and Linux operating systems will already have terminals installed. Simply search for 'Terminal' and/or look for the terminal icon.<br> 
![terminal icon](../fig/terminal.png)


1. Open the terminal and type the following command substituting 'ip_address' for the ip address your instructor will provide (or the ip address of an instance you have provisioned yourself). *Be sure to pay attention to capitalization and spaces*

        $ ssh dcuser@ip_address
        
2. You will receive a security message that looks something like the message below. Type 'yes' to proceed.

        The authenticity of host 'ec2-52-91-14-206.compute-1.amazonaws.com (52.91.14.206)' can't be established.
        ECDSA key fingerprint is SHA256:S2mMV8mCThjJHm0sUmK2iOE5DBqs8HiJr6pL3x/XxkI.
        Are you sure you want to continue connecting (yes/no)?

3. In the final step, you will be asked to provide a login and password. **Note:** When typing your password, it is common in Unix/Linux not see see any asterisks (e.g. ****) or moving cursors. Just continue typing.
4. You should now be connected!

</div>




<div id='div_cyverse' style="display:none" markdown="1">

CyVerse!!

- are MD lists formatted properly?
- list item 2?

* what about bullet ones?
* bullet item 2?

**bold** items go Here

* emphasized items here *

`quoting code`

> a block section of quoted text

and an in-line URL and anchor to [the DataCarpentry website](http://www.datacarpentry.org/)

</div>



<div id='div_hpc' style="display:none" markdown="1">

HPC Cluster!!

</div>



