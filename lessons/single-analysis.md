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

### Interpret FASTQC results

Let's have a look at the results.

````
<AWESOME BOXPLOT>
````

This is the boxplot analysis for your FASTQ data. Phred quality score is on the ordinate axis.  The purpose of this plot is to look at the overall quality of the seuqence

```
<COOL TILE PLOT>
```

This is a tile plot for your FASTQ data. The purpose of this plot is to determine whether problems were encountered during sequencing

```
<AMAZING OTHER STUFF>
```
### Possible Quality Issues

Some problems you might encounter.  A nice summary of issues can be found at:

* [Good sequence run](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/good_sequence_short_fastqc.html)
* [Bad sequence run](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/bad_sequence_fastqc.html)
* [RNA-Seq](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/RNA-Seq_fastqc.html)
* [Small RNA](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/small_rna_fastqc.html)

The last two are examples where failing tests do not mean the sample is bad (depends on the technology, experiment, etc)

*Question* : Are any Illumina adapters present in your data?

### Analysis complete (?)

Wait, you have other files to analyze.  Can you do this in a better way?

