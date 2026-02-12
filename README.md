# Assignment 2

## Overview
In this assignment, you will build a **Snakemake workflow** to process next-generation sequencing (NGS) data. You will perform quality control on FASTQ files and map the reads to a reference genome. This assignment will help you develop reproducible bioinformatic pipelines using Snakemake.

## Learning Objectives
By completing this assignment, you will:
- Understand the basics of Snakemake workflow syntax
- Implement quality control steps for NGS data
- Map sequencing reads to a reference genome
- Generate summary statistics and reports
- Practice writing reproducible computational workflows

## Prerequisites
Before starting this assignment, ensure you have the following installed:
- Python 3.8+
- [Snakemake](https://snakemake.readthedocs.io/) (v7.0+)
- [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)
- [MultiQC](https://multiqc.info/)
- [Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml)
- [SAMtools](http://www.htslib.org/)

You can install most tools using conda/mamba:
```bash
mamba create -n assignment-2-env -c bioconda -c conda-forge snakemake fastqc multiqc bowtie2 samtools
conda activate assignment-2-env
```

## Data
Your sequencing data is located in the `data/fastq/` directory. You will find:
- Paired-end FASTQ files (`.fastq.gz` format)
- Naming convention: `{sample}_R1.fastq.gz` and `{sample}_R2.fastq.gz`
- Reference genome in `data/reference/` directory

## Assignment Tasks

### Task 1: Quality Control
Implement Snakemake rules to:
1. Run **FastQC** on all FASTQ files (both R1 and R2)
2. Aggregate QC reports using **MultiQC**
3. Save outputs to `results/qc/`

#### Expected outputs:
- `results/qc/fastqc/{sample}_R1_fastqc.html`
- `results/qc/fastqc/{sample}_R2_fastqc.html`
- `results/qc/multiqc_report.html`

### Task 2: Read Mapping
Implement Snakemake rules to:
1. Index the reference genome (if not already indexed)
2. Map reads to the reference genome using **Bowtie2**
3. Convert SAM to BAM format and sort using **SAMtools**
4. Index the sorted BAM files
5. Generate mapping statistics

#### Expected outputs:
- `results/mapped/{sample}.sorted.bam`
- `results/mapped/{sample}.sorted.bam.bai`
- `results/stats/{sample}.flagstat.txt`

### Task 3: Workflow Configuration
Create a proper Snakemake workflow structure:
1. Use a `Snakefile` with clear rule definitions
2. Create a `config.yaml` file for configurable parameters
3. Use wildcards to handle multiple samples
4. Define an `all` rule that specifies final outputs

### Task 4: Documentation
Document your workflow:
1. Add comments to your Snakefile explaining each rule
2. Create a brief report (1-2 paragraphs) summarizing:
   - Overall read quality
   - Mapping rates
   - Any quality concerns

## Workflow Structure
Your final directory structure should look like:
```
.
├── workflow/
│   └── Snakefile
├── config/
│   └── config.yaml
├── data/
│   ├── fastq/
│   │   ├── sample1_R1.fastq.gz
│   │   ├── sample1_R2.fastq.gz
│   │   └── ...
│   └── reference/
│       └── genome.fa
├── results/
│   ├── qc/
│   │   ├── fastqc/
│   │   └── multiqc_report.html
│   ├── mapped/
│   │   ├── sample1.sorted.bam
│   │   └── sample1.sorted.bam.bai
│   └── stats/
│       └── sample1.flagstat.txt
└── report.md
```

## Running Your Workflow
Execute your workflow with:
```bash
# Dry-run to check workflow
snakemake --dry-run

# Generate workflow diagram
snakemake --dag | dot -Tpng > dag.png
```

## Deliverables
Submit the following via GitHub by merging your working branch into the main branch via a pull request:
1. `workflow/Snakefile` - Your complete workflow
2. `config/config.yaml` - Configuration file
3. `report.md` - Brief analysis report
4. `dag.png` - DAG visualization of your workflow

**Do not commit large data files or BAM files to GitHub!** Use `.gitignore` appropriately.

## Tips
- Start small: test your workflow one rule at a time
- Use `snakemake --dry-run` frequently to check for errors
- Review the [Snakemake tutorial](https://snakemake.readthedocs.io/en/stable/tutorial/tutorial.html)
- Make sure to add the results and .snakemake directories to your `.gitignore` file to avoid committing large files

## Resources
- [Snakemake Documentation](https://snakemake.readthedocs.io/)
- [FastQC Manual](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)
- [Bowtie2 Manual](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml)
- [SAMtools Documentation](http://www.htslib.org/doc/samtools.html)

## Due Date
**Friday, February 20th at 5pm**


