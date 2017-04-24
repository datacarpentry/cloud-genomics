---
title: "Introduction"
teaching: 0
exercises: 0
questions:
- What is cloud computing?
- How do I log into a remote server?
objectives:
- Understand benefits of working on a remote computer system
- Be able to connect to a cloud instance via SSH or VNC
- Check the available resources and file system on your remote machine
- Keep background processes working in the cloud with `tmux`
---

<script language="javascript" type="text/javascript">

//USING FOR LOOP

// Note: This will only work in platforms that have
// implemented NodeList.prototype[Symbol.iterator]
function setClassDisplayMode(className, displayValue){
    var classList = document.getElementsByClassName(className);
    for (let oneItem of classList) {
        oneItem.style.display = displayValue
}

function set_page_view_defaults() {
    setClassDisplayMode('div_aws', 'block');
    setClassDisplayMode('div_cyverse', 'none');
    setClassDisplayMode('div_hpc', 'none');
};

function change_content_by_platform(form_control){
    if (!form_control || document.getElementById(form_control).value == 'aws') {
        set_page_view_defaults();
    } else if (document.getElementById(form_control).value == 'cyverse') {
        setClassDisplayMode('div_aws', 'none');
        setClassDisplayMode('div_cyverse', 'block');
        setClassDisplayMode('div_hpc', 'none');
    } else if (document.getElementById(form_control).value == 'hpc') {
        setClassDisplayMode('div_aws', 'none');
        setClassDisplayMode('div_cyverse', 'none');
        setClassDisplayMode('div_hpc', 'block');
    } else {
        alert("Error: Missing platform value for 'change_content_by_platform()' script!");
    }
}

window.onload = set_page_view_defaults;
</script>


The cloud is a part of our everyday life (e.g. using Amazon, Google, Netflix, or an ATM involves remote computing). The topic is fascinating but this lesson says '5 minutes or less' so let's get connected. 

**Please select the platform you wish to use for the exercises: <select id="id_platform" name="platformlist" onchange="change_content_by_platform('id_platform');return false;"><option value="aws" id="id_aws" selected> AWS </option><option value="cyverse" id="id_cyverse"> CyVerse </option><option value="hpc" id="id_hpc"> HPC/HTC cluster </option></select>**

## Exercises

### **A. Connecting to a remote machine via SSH**

This is the first and last place in these lessons where it will matter if you are using PC, Mac, or Linux. After we connect, we will all be on the same operating system/computing environment. 

<div class="div_aws" style="display:block" markdown="1">

> To save time, your instructor will have launched an remote computer (instance) for you prior to the workshop. If you are following these lessons on your own, or after the workshop see the lesson on [launching cloud instances on your own](../discuss/) for instructions on how to do this yourself. 

**User Credentials**
Credentials are case sensitive:

- Username: dcuser
- Password: data4Carp

</div>

some text in-between

<div class='div_cyverse' style="display:none" markdown="1">

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

some text in-between #2

<div class='div_hpc' style="display:none" markdown="1">

HPC Cluster!!

</div>

some text in-between #3

<div class='div_aws' style="display:block" markdown="1">

Another AWS section

</div>

some text in-between #4

<div class='div_cyverse' style="display:none" markdown="1">

Another Cyverse section

</div>
