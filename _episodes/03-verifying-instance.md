---
title: "Fine tuning your Cloud Setup"
teaching: 5
exercises: 10
questions:
- Is my remote computer correctly configured?
- How do I keep my processing going when I leave?
objectives:
- Check the available resources and file system on your remote machine
- Keep background processes working in the cloud with `tmux`
keypoints:
- Always check a new instance to verify it started correctly
- Using a program like `tmux` can keep your work going even if your internet connection is bad
---

# Is this the right cloud?

Once you're connected to your new remote instance, it's a good idea to double check that
the settings are what you wanted, and that everything is working smoothly before you start
your project.

For this workshop, your instructor did all the verification before the workshop
even started, but this is an important skill for when you start running your own instances.


## Verifying your connection

When you connect, it is typical to receive a welcome screen. The Data Carpentry Amazon instances display this message upon connecting:

~~~
Welcome to Ubuntu 14.04.3 LTS (GNU/Linux 3.13.0-48-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Sun Jan 24 21:38:35 UTC 2016

  System load:  0.0                Processes:           151
  Usage of /:   48.4% of 98.30GB   Users logged in:     0
  Memory usage: 6%                 IP address for eth0: 172.31.62.209
  Swap usage:   0%

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

12 packages can be updated.
10 updates are security updates.


Last login: Sun Jan 24 21:38:36 2016 from
~~~
{: .output}

You should also have a blinking cursor awaiting your command

~~~
$
~~~
{: .bash}

## Verifying your environment

Now that we have connected here are a few commands that tell you a little about the machine you have connected to:

- `whoami` - shows your username on computer you have connected to:

~~~
$ whoami
~~~
{: .bash}

~~~
dcuser
~~~
{: .output}

-  `df -h` - shows space on hard drive*

~~~
dcuser@ip-172-31-62-209 ~ $ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            2.0G   12K  2.0G   1% /dev
tmpfs           396M  792K  395M   1% /run
/dev/xvda1       99G   48G   47G  51% /
none            4.0K     0  4.0K   0% /sys/fs/cgroup
none            5.0M     0  5.0M   0% /run/lock
none            2.0G  144K  2.0G   1% /run/shm
none            100M   36K  100M   1% /run/user
~~~
{: .output}

\* Under the column 'Mounted on' row that has '/' as the value shows the value for the main disk.

- `cat /proc/cpuinfo` - shows detail information on how many processors (CPUs) the machine has

~~~
dcuser@ip-172-31-62-209 ~ $ cat /proc/cpuinfo
processor  : 0
vendor_id	: GenuineIntel
cpu family	: 6
model		: 62
model name	: Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz
stepping	: 4
microcode	: 0x415
cpu MHz		: 2494.060
cache size	: 25600 KB
physical id	: 0
siblings	: 2
core id		: 0
cpu cores	: 2
apicid		: 0
initial apicid	: 0
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology eagerfpu pni pclmulqdq ssse3 cx16 pcid sse4_1 sse4_2 x2apic popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm xsaveopt fsgsbase smep erms
bogomips	: 4988.12
clflush size	: 64
cache_alignment	: 64
address sizes	: 46 bits physical, 48 bits virtual
power management:

processor	: 1
vendor_id	: GenuineIntel
cpu family	: 6
model		: 62
model name	: Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz
stepping	: 4
microcode	: 0x415
cpu MHz		: 2494.060
cache size	: 25600 KB
physical id	: 0
siblings	: 2
core id		: 1
cpu cores	: 2
apicid		: 2
initial apicid	: 2
fpu		: yes
fpu_exception	: yes
cpuid level	: 13
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology eagerfpu pni pclmulqdq ssse3 cx16 pcid sse4_1 sse4_2 x2apic popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm xsaveopt fsgsbase smep erms
bogomips	: 4988.12
clflush size	: 64
cache_alignment	: 64
address sizes	: 46 bits physical, 48 bits virtual
power management:
~~~
{: .output}

- `tree -L 1` - shows a tree view of the file system 1 level below your current location.

~~~
$ tree -L 1
~~~
{: .bash}

~~~
├── dc_sample_data
├── Desktop
├── Downloads
├── FastQC
├── openrefine-2.6-beta.1
├── R
└── Trimmomatic-0.32

7 directories, 0 files
~~~
{: .output}

## Staying Connected to the Cloud

Depending on how you connect to the cloud, you may have processes and jobs that are
running, and will need to continue running for some time. If you have connected to your
cloud desktop via VNC, jobs you start will continue to run. If you are connecting via SSH,
if you end the SSH connection (e.g. you exit your SSH session, you lose your connection
to the internet, you close your laptop, etc.), jobs that are still running when you
disconnect will be killed. There are a few ways to keep cloud processes running in the background.
Many times when we refer to a background process we are talking about what is
[described at this tutorial](http://www.cyberciti.biz/faq/linux-command-line-run-in-background/) -
running a command and returning to shell prompt. Here we describe a program that will
allow us to run our entire shell and keep that process running even if we disconnect: `tmux`. If you don't have `tmux` on your system, you should still be able to use `screen`, instructions for which are provided below.

### tmux


#### Starting and attaching to `tmux` sessions

**Starting a new session**

A 'session' can be thought of as a window for `tmux`, you might open an terminal to do one thing on the a computer and then open a new terminal to work on another task at the command line. You can start a session and give it a descriptive name:

~~~
$ tmux new -s session_name
~~~
{: .bash} 

This creates a session with the name 'session_name'

As you work, this session will stay active until you close this session. Even if you disconnect from your machine, the jobs you start in this session will run till completion.

**Seeing active sessions**

If you disconnect from your session, or from your ssh into a machine, you will need to reconnect to an existing `tmux` session. You can see a list of existing sessions:

~~~
$ tmux list-sessions
~~~
{: .bash} 

**Connecting to a session**

To connect to an existing session:

~~~
$ tmux attach -t session_name
~~~
{: .bash} 

The `-t` option = 'target'

**Switch sessions**
You can switch between sessions:

~~~
$ tmux switch -t session_name
~~~
{: .bash}

**Kill a session**
You can end sessions:

~~~
$ tmux kill-session -t session_name
~~~
{: .bash}

### screen

This is another program that has mostly the same capabilities as tmux. It's a lot older, though, so can be more clunky to use; however, it is likely to be available on any cloud system you encounter.

#### Starting and attaching to `screen` sessions

**Starting a new session**

A 'session' can be thought of as a window for `screen`, you might open an terminal to do one thing on the a computer and then open a new terminal to work on another task at the command line. You can start a session and give it a descriptive name:

~~~
$ screen -S session_name
~~~
{: .bash}

This creates a session with the name 'session_name'

As you work, this session will stay active until you close this session. Even if you disconnect from your machine, the jobs you start in this session will run till completion.

**Detach session (process keeps running in background)**

You can detach from a session by pressing `control + a` followed by `d` (for detach) on your keyboard. 

**Seeing active sessions**

If you disconnect from your session, or from your ssh into a machine, you will need to reconnect to an existing `screen` session. You can see a list of existing sessions:

~~~
$ screen -ls
~~~
{: .bash}

**Reconnecting to a session**

To reconnect to an existing session:

~~~
$ screen -r session_name
~~~
{: .bash}

The `-r` option = 'resume  a detached screen session'

**Kill a session**
To end a session, type `exit` after reconnecting to the session:

~~~
$ screen -r session_name
$ exit
~~~
{: .bash}
