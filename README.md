# Snakemake Workflow for 4C-ker

*4C-Workflow* is a snakemake implementation for the *4C-ker* library.
This generalized workflow aims to automate the 4C data analysis process allowing
you to get to your results faster. To that end, the workflow supports multiple 
baits and comparisons by simply specifying the baits and comparisons within the 
*config* file.

This workflow depends heavily upon *Miniconda*, *R.4Cker*, and *Snakemake* so if you
want know what they are checkout the links below. Otherwise just follow the **setup**
process and you should be able to get *4C-Workflow* up and running.

* [Miniconda](http://conda.pydata.org/miniconda.html)
* [R.4Cker Github](https://github.com/rr1859/R.4Cker)
* [4C-ker Paper](http://journals.plos.org/ploscompbiol/article?id=10.1371%2Fjournal.pcbi.1004780)
* [Snakemake](https://bitbucket.org/snakemake/snakemake/wiki/Home)

## Contents
- [Setup](#setup)
  - [4C-Workflow](#4c-workflow)
  - [Analysis](#analysis)
- [Run](#run)
- [Example](#example)

## Setup

You may have noticed that the setup process consists of two sections 
**4C-Workflow** and **Analysis**. *4C-Workflow* guides you through the setup
process of getting the various parts of the 4C pipeline working. *Analysis* 
will show you how to describe your experiment to 4C-Workflow thus enabling it 
to perform an accurate analysis. 

### 4C-Workflow

1. `git clone` the *4C-Workflow* directory into your local directory
2. Install [Miniconda](http://conda.pydata.org/miniconda.html)
3. Once installed use the terminal to create a conda environment while inside 
   the *4C-Workflow* folder
   - `conda create --name 4C-Workflow --file environment.txt`
4. Within terminal perform the following commands to install *R.4Cker*:
   - `source activate 4C-Workflow`
   - `R`
   - `library(devtools)`
   - `install_github("rr1859/R.4Cker")`

You are now ready to use *4C-Workflow* to analyze your raw 4C data.

### Analysis

1. *Snakemake* uses the *config.yaml* file to understand the experimental 
   parameters, personalize it accordingly
   - The file is divided into four general blocks:
	 - **comparisons**
	   - Raw bedGraphs for each of the experimental comparisons are placed here
	    - Make sure to follow the **exact formatting** displayed in the example
	    - **Don't forget** to change the *names* for each of the comparisions
		  - **Note:** Each of the conditions in the example have two replicates
		  - *bedGraph/* is the folder that *Snakemake* will place the files into
	 - **samples**
	   - *Snakemake* will use the path name to find all the raw *.fastq* files
	   - Make sure to insert the **full path** to your *.fastq* files
	 - **baits**
	     - *bait_chr*: short form of the chromosome name
	     - *bait_coord*: numerical start site for your primer, usually after 
		   restriction enzyme site
	     - *bait_name*: the shortform bait name
	     - *primary_enz*: sequence of the primary enzyme
	     - *fragment_len*: barcode + primer + primary restriction enzyme, eg. 37
	     - *primer*: genome sequence for the primer
	 - **reference_genome**
	    - *name*: shortform name of reference genome
	    - *location*: location of reference genome file
		 - *species*: shortform species name
2. Lastly add both a *.fasta* reference genome and primary enzyme sequence to 
   the *reduced_genome* folder
   - **Make Sure** the names for both the reference genome and enzyme match the 
	 names provided for *primary_enz_name* and *reduced_genome* from **other**
	 - eg. dm6 == dm6.fasta & hindiii == hindiii.fasta

## Run

1. Finally open the terminal and while inside the *4C-Workflow/* folder run the 
   following command:
   - `sh runscript`
2. Wait for the analysis to finish and find your results in the *Output/* folder
   - Either IGV or UCSC Genome Browser can be used to view the .bedGraph and 
	 .bed files.
	 
## Example

The example *config.yaml* is setup to handle an experiment with two baits,
*someBait1* and *someBait2*, and three comparisons, *mock_vs_condition1*, 
*mock_vs_condition2* and *condition1_vs_condition2*. The basic organizational
structure of this example is key to getting an experiment with any number of 
*baits* or *comparisons* analyzed. Please note that deviating from this
structure will likely cause *4C-Workflow* to complain and stop working. Now 
before analyzing your own data I recommend that you follow the example below 
to get a basic 4C-Workflow pipeline to work. 

### Download Raw Fastq Files

Assuming that you have already performed `git clone` on the *4C-Workflow*
directory, you will notice the following folder organization: 

  .  
	├── reduced_genome  
    ├── raw_data  
    │      └── hindiii.fa  
    ├── 4C.R  
	├── Snakefile  
	├── config.yaml  
	├── environment.txt  
	├── runscript  
	└──  README.md  

### Setup *config.yaml*



## Acknowledgements

This pipeline would not have been possible without the constant guidance from 
	[Ryan Dale](https://github.com/daler) and the awesome resources at the NIH.
