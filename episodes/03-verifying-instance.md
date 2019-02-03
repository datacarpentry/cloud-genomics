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

  System information as of Tue Jan 29 22:28:18 UTC 2019

  System load:  0.04               Processes:           164
  Usage of /:   43.1% of 98.30GB   Users logged in:     0
  Memory usage: 2%                 IP address for eth0: 172.31.41.107
  Swap usage:   0%

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

New release '16.04.5 LTS' available.
Run 'do-release-upgrade' to upgrade to it.
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
  dcuser@ip-172-31-62-209 ~ $ whoami
  dcuser
  ~~~
  {: .output}

- `df -h` - shows space on hard drive

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

  Under the column 'Mounted on row' that has `/` as the value shows the value for the main disk

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
  dcuser@ip-172-31-62-209 ~ $ tree -L 1
  .
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
running, and will need to continue running for some time. If you are connecting to your
cloud desktop via VNC, jobs you start will continue to run. If you are connecting via SSH,
if you end the SSH connection (e.g. you exit your SSH session, you lose your connection
to the internet, you close your laptop, etc.), jobs that are still running when you
disconnect will be killed. There are a few ways to keep cloud processes running in the background.
Many times when we refer to a background process we are talking about what is
[described at this tutorial](http://www.cyberciti.biz/faq/linux-command-line-run-in-background/) -
running a command and returning to shell prompt. Here we describe a program that will
allow us to run our entire shell and keep that process running even if we disconnect: `tmux`. If you don't have `tmux` on your system, you should still be able to use `screen`. This is another program that has mostly the same capabilities as `tmux`. It's a lot older, though, so can be more clunky to use; however, it is likely to be available on any cloud system you encounter.

In both `tmux` and `screen`, you open a 'session'. A 'session' can be thought of as a window for `tmux` or `screen`, you might open an terminal to do one thing on the a computer and then open a new terminal to work on another task at the command line. 

As you work, an open session will stay active until you close this session. Even if you disconnect from your machine, the jobs you start in this session will run till completion.

### Starting and attaching to a session

You can start a session and give it a descriptive name:

- `tmux`

  ~~~
  $ tmux new -s session_name
  ~~~
  {: .bash}

- `screen`

  ~~~
  $ screen -S session_name
  ~~~
  {: .bash}

This creates a session with the name `session_name` which will stay active until you close it.

### Detach session (process keeps running in background)

You can detach from a session by pressing on your keyboard:

- `tmux`: `control + b` followed by `d` (for detach)
- `screen`: `control + a` followed by `d` (for detach)

#### Seeing active sessions

If you disconnect from your session, or from your ssh into a machine, you will need to reconnect to an existing session. You can see a list of existing sessions:

- `tmux`

  ~~~
  $ tmux list-sessions
  ~~~
  {: .bash}

- `screen`

  ~~~
  $ screen -ls
  ~~~
  {: .bash}

#### Connecting to a session

To connect to an existing session:

- `tmux`

  ~~~
  $ tmux attach -t session_name
  ~~~
  {: .bash} 

  The `-t` option = 'target'

- `screen`

  ~~~
  $ screen -r session_name
  ~~~
  {: .bash}

  The `-r` option = 'resume  a detached screen session'

#### Switch sessions

You can switch between sessions:

- `tmux`

  ~~~
  $ tmux switch -t session_name
  ~~~
  {: .bash}

#### Kill a session

You can end sessions:

- `tmux`

  ~~~
  $ tmux kill-session -t session_name
  ~~~
  {: .bash}

- `screen`

  ~~~
  $ screen -r session_name
  $ exit
  ~~~
  {: .bash}


### Installing additional software

By default `tmux` is not installed in most cloud Linux instances. However you can install new software packages using Package Managers like YUM (for Red Hat and Centos instances) or APT (for Debian or Ubuntu instances). We will explore how to install `tmux` using APT (Advanced Package Tool).

####  Update APT

Before installing or upgrading any system packages, you should always update the local APT cache:

~~~
$ sudo apt-get update
Hit:1 http://au.archive.ubuntu.com/ubuntu xenial InRelease
Get:2 http://au.archive.ubuntu.com/ubuntu xenial-updates InRelease [102 kB]
...
Fetched 3,413 kB in 1s (2,233 kB/s)
Reading package lists... Done
~~~
{: .bash}

#### Search for APT packages using including software

Most common software tools will have a package named the same, but this is not always the case. If you know the name of the program you wish to install, but are not sure of the package name, you can use the `apt` program to search packages:

~~~
$ sudo apt search tmux
Sorting... Done
Full Text Search... Done
abduco/xenial 0.1-2 amd64
  terminal session manager

powerline/xenial-updates 2.3-1ubuntu0 amd64
  prompt and statusline utility

tmate/xenial 1.8.10-2build1 amd64
  terminal multiplexer with instant terminal sharing

tmux/xenial,now 2.1-3build1 amd64
  terminal multiplexer

tmuxinator/xenial 0.7.0-2 all
  Create and manage tmux sessions easily
$
~~~
{: .bash}

There is a plain `tmux` package, so we will use that to install.

#### Install packages using APT

Once you know the package name, you can install it using `apt-get install`:

~~~
$ sudo apt-get install tmux
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  libevent-2.0-5 libutempter0
The following NEW packages will be installed:
  libevent-2.0-5 libutempter0 tmux
0 to upgrade, 3 to newly install, 0 to remove and 0 not to upgrade.
Need to get 345 kB of archives.
After this operation, 949 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://mirror.overthewire.com.au/ubuntu xenial-updates/main amd64 libevent-2.0-5 amd64 2.0.21-stable-2ubuntu0.16.04.1 [114 kB]
Get:2 http://mirror.overthewire.com.au/ubuntu xenial/main amd64 libutempter0 amd64 1.1.6-3 [7,898 B]
Get:3 http://mirror.overthewire.com.au/ubuntu xenial/main amd64 tmux amd64 2.1-3build1 [223 kB]
Fetched 345 kB in 0s (863 kB/s)
(Reading database ... 130583 files and directories currently installed.)
...
Setting up libevent-2.0-5:amd64 (2.0.21-stable-2ubuntu0.16.04.1) ...
Setting up libutempter0:amd64 (1.1.6-3) ...
Setting up tmux (2.1-3build1) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...
~~~
{: .bash}

When this has completed, `tmux` will now be available for use on the instance.
