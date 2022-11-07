# Performing basic QC for files
## Request a full node in Owens
```shell
sinteractive -c 28 -t 00:15:00 -J QC -A PAS2303
```
## Go to directory QC:
```shell
/fs/ess/scratch/PAS2303/Your_OSC_ID/Microbiomes/QC
mkdir FastQC_reports MultiQC_reports

# extracting fastq files from Raw_Data
find /fs/ess/scratch/PAS2303/Your_OSC_ID/Microbiomes/Raw_Data/reads_fastq/ -name "*fastq.gz" -exec cp {} . \;
ls *fastq.gz
```

## We will start with the QC of the data using FastQC and MultiQC:
```shell
apptainer exec ../Software/FastQC.sif fastqc *fastq.gz --outdir=FastQC_reports
apptainer exec ../Software/MultiQC.sif multiqc FastQC_reports --interactive -o MultiQC_reports
# Check your reports. Do you notice something you should be worried about?
```

# You will need to produce a tab separated file file with then ames of the samples (check the file used to download the data) and with the paths get the files, the file should look like the lines below (first line are headers). It is called manifest file:
```
sample-id   forward-absolute-filepath   reverse-absolute-filepath
sample-1    filepath/sample0_R1.fastq.gz    filepath/sample1_R2.fastq.gz
sample-2    filepath/sample2_R1.fastq.gz    filepath/sample2_R2.fastq.gz
sample-3    filepath/sample3_R1.fastq.gz    filepath/sample3_R2.fastq.gz
sample-4    filepath/sample4_R1.fastq.gz    filepath/sample4_R2.fastq.gz

# Getting basic files
ls *_1.fastq.gz > paths_1.txt
ls *_2.fastq.gz > paths_2.txt
```
