# TrainingSetGeneration-HalfonLab
Halfon Lab-specific versions of the Training Set generation workflow

(c) Marc Halfon

Date: October 2024

Based on

#####################################################

****** Training set construction pipeline ********

(c) Hasiba Asma

Date: Jan 2020

updated: Oct 2021 (edited readme, fixed snakemake file)

This pipeline follows all the steps mentioned in 3.2 section of protocol (Kazemian & Halfon 2019). 
A bed file of known CRMs from melanogaster as input is needed, and then pipeline grabs its orthologs (using liftover) from other species, repeats masked, also generate negative set, and returns us the final fasta files of positive (CRMs) and negatives (background sequences) to be used with SCRMshaw. 

#####################################################

**Steps to follow:**
1.	Git clone this folder to your directory on ccr/cluster
2.	Place the .bed files for your new training set(s) into the "in" directory
3.	Note: .bed files should be sorted (e.g., bedtools sort -i _file.bed_ and chromosome names MUST begin with 'chr'.
4.	If desired, update the --mail-user and the --time parameters in the Slurm script (tset_slurm_wrapper.sh). A good estimate for time is about 5 minutes per training set. 
5.	Run the following command:
    $ sbatch tset_slurm_wrapper.sh in/
6.  An output directory with the name of each training set will be created, with two files as the final output, "crms.fasta" and "neg.fasta" (it's a good idea to double check that these have correct number of headers, e.g. using "grep -c '>' "; there should be roughly 10x the number as the number of sequences in the original training CRMs .bed file)  	
