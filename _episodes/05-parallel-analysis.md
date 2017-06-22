---
title: "Parallel analysis"
teaching: 0
exercises: 0
questions:
- "Why would we use parallel computing?"
- "How can we use parallel computing?"
objectives:
- "List the advantages of parallel computing as compared to serial computing."
- "Determine if your analysis can take advantage of multiple CPU cores."
- "Differentiate between a process and a thread in relation to CPU cores."
- "Define the terms *process* and *job*."
- "Monitor and kill processes."
- "Run programs in the foreground and in the background."
- "Describe best practices for running multiple analyses at once (from multiple screens to background)"
- "Launching programs via gnu_parallel"
- "(HPC) Run programs as jobs on a cluster."
- "(HPC) Run programs as jobs via a job scheduler."

keypoints:
- "Parallel computing saves time with concurrent processing."
---


## Starting a Parallel Analysis

### Running a number of programs serially

In order to perform the same operation over a number of files, we can encompass the group of files and iterate over each one to run a given command. We use a 'for loop', a programming construct common to many languages, to perform this. We combine this with filename wildcards and a shell variable to hold the filename on each iteration to do the work:

    for file in *.fq; do 
     echo $file
     fastqc $file -o ${file}_out
    done

Each iteration through the loop, the variable `file` will hold the next fastq file in the directory, we will print the filename to the screen, and then run FastQC on it. As we've seen in the shell lessons, to assign the variable we simply use the variable name `file`. To represent the value of the variable, use `$file`. If you wish to embed the variable in text (e.g. xxx_out), it's best to use an alternate form `${file}`. 

### Running a number of programs simultaneously

We have several problems with this approach. Your computer is busy running these and you don't have the opportunity to do any additional work. And you computer does each execution in order. Not very efficient.

How can we speed this up? 

As we learned in the Unix shell lesson, when running a program, it is possible to have the program run in the background, so that the command prompt returns and you can continue typing. You do this using the '&' symbol at the end of your command:

    sleep 500 &

The shell returns a number ID for that program in memory. This is the ID of the process -- the instance of the program in memory with the environment that the unix shell creates to track how it runs.

**Exercise: How can we run the same script (for loop) as above so that we run all the analyses simultaneously?**

    for file in *.fq; do 
     echo $file
     fastqc $file &
    done

So, if we can put things in the background, why not put everything in the background? Well, as it turns out, there are limits. The Unix shell will attempt to spread out the processes onto as many CPU cores that it has at hand so that the programs run in parallel. But what if you do'nt have enough cores to match the number of programs run? In that case, the unix kernel (the master scheduler) will give each process a slice of time to run, then switch them out constantly in order to let all the programs run. This results in reduced performance, and your programs will run more slowly (than expected)

*Best practice: match the number of simultaneously run background processes to the number of cores that you have*

You can watch what is going on with your processes using the `top` command. The top command will show program name, RAM, CPU usage, and other metrics. The stats shown will vary from system to system.

**Exercise:  What commands can use you to see your process IDs?**

**Exercise:  Determine how much RAM your fastqc programs are running?**

Topic: process vs. thread (is your application threaded and can I tell?)


### Job management (local, queued)

* (local) ps, top
* (scheduler) slurm commands

### GNU parallel

* writing your control file
* options for cloud/cluster deployment

### ? Python multiprocessing; Rparallel; Rbatchjobs; Rmpi; Rsnow

