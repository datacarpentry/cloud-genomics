### Now let's start an analysis

* Use `top` to determine whether other resources are being run at the moment
 * Do you have enough resources for your work?

```
INSERT TOP WINDOW
```

### Now let's start an analysis

* We're going to run FASTQC on a single FASTQ file we downloaded previously
  * Prior to starting should we set up a work directory for this?
  * We can add this as an option to FASTQC
  * ...but where is FASTQC?
  * Is it in your PATH?

```
# CODE HERE TO ADD FASTQC TO PATH?
fastqc <PATH TO FOO.FASTQ> -o <WORKDIR>
```

### FASTQC Results

Note that the output is in a specific working directory, and is present at both an HTML file and a `*.zip` file

How do you open the HTML file?

```
# Remote Server
# where is your data?
pwd
```

```
# Your laptop
scp <REMOTE_URL:location of HTML file> <LOCAL DIRECTORY>
```

Open the file:

```
<FASTQC example?>
```

### Should we have a bit on how to interpret a FASTQC analysis here, or should this occur later?

### Analysis complete (?)

Wait, you have other files to analyze.  Can you do this in a better way?

