# crypto-QTL-paper
Scripts and analysis of _C. deneoformans_ cross between XL280 X 431, as described in [Roth et al. (2021)](https://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1009313).

## Software used in this  study

**Python (anaconda) v 3.7.3**
- Used for analysis and visualization

**[BWA](http://bio-bwa.sourceforge.net/)**
- Used to align FASTQ file to an XL280 reference genome

**[Samtools](http://www.htslib.org/)**
- Used to generate and filter SAM and BAM files

**[Bamaddrg](https://github.com/ekg/bamaddrg)**
- Used to add read group information to BAM

**[Freebayes](https://github.com/freebayes/freebayes) haplotype caller**
- Used to detect genetic variants segregating in the mapping population

**[BLAT](https://genome.ucsc.edu/FAQ/FAQblat.html)**
- The blast like alignment tool

## Description of scripts 

### Aligning paired reads, make SAM and BAM files

**Generate-samtobam-freebayes-scripts.ipynb****
- Generates bash commands for aligning FASTQ files.
- See data availability statement for SRA numbers to raw FASTQ files.

Input: paired FASTQ files

Output: Bash commands for alignment and SAM to BAM generation
    
**Align-FASTQ-to-sam.sh**
- List of BWA commands used to align pair-read data.

Input: paired FASTQ files

Output: SAM files per sample

**Sort-sam-to-bam.sh** 
- Via samtools, sorts SAM files and covert them to BAM files.

Input: SAM file per sample

Output: BAM file per sample

**Add-read-group-to-bam.sh**
- Appends read group information per BAM file.

Input: BAM files

Output: BAM files with read group information added

**Add-bam-index.sh**
- Adds index to BAM files via samtools.

Input: BAM files with read group inforomation added

Output: Modified BAM files and BAI index file (per BAM)

#### Freebayes commands for variant calling

**Run-freebayes1.sh**
**Run-freebayes2.sh**
**Run-freebayes3.sh**
- List of commands used to call variants using the Freebayes Haplotype Caller.
- Commands are in three batches with each separated across chromosomes.

Input: Reference genome (xl280genome.fasta), list of sorted BAM files with read groups

Output: a VCF file for each of the 14 chromosomes

### Parse and filter VCFs, non-synonymous variant detection

**Make chromosome map.ipynb**
- Generates a dataframe (CSV) with genomeic length and cumulative lengths of chromosomes

Input: xl280genome.fasta, the XL280 reference genome

Output: XL280-chrom-map.csv

**VCF to dataframes.ipynb**
- Parses each VCF to a set of dataframes (CSV) used in further processing.

Input: VCF per chromosome

Output: Two dataframes per chromosome with genothype and read depth information

**Aggregate and collect dataframes.ipynb**
- Combines the dataframes generated above into two data sets

Input: Genotype and allelic depth dataframes per chromosome

Output: Genotype and Allelic read depth dataframes (CSV) combined across chromosomes with the names CDx-ill-gvs.csv.gz and CDx-ill-ads.csv.gz

**Filter genetic variants.ipynb**
- Filters genetic variants based on depth, allele frequency, and callrate.

Inputs: CDx-ill-gvs.csv.gz and CDx-ill-ads.csv.gz

Output: Dataframe of filtered variants named, CDx-ill-SNP-INDEL-df-104.csv

**SNPeffect.ipynb**
- Predicts the effects of variants on annotated genes

**Gene_analysis.ipynb**
- Analysis of non-synonymous changes within QTL

### Phenotype data processing and analysis

**Growth curve data curation.ipynb**
- Curates growth curve data generated on TECAN plate readers

**Baselining growth curves.ipynb**
- Calculates and subtracts baseline growth profile across samples

**Median filtering growth curves.ipynb**
- Filters growth profiles via a recursive median filter

**Baselining XL280 ssk1 knockouts.ipynb**
- Baselines growth profiles of ssk1 knockouts in the XL280 strain background.

**H2O2_epistasis_discrete.ipynb**
- Information gain analysis of hydrogen peroxide growth phenotypes

**Fine_mapping_fludioxonil_analysis.ipynb**
- Analysis of fludioxonil phenotypes in the additional fine-mapped progeny

### Scripts that make the ten main figures in Roth et al.

**Melanin_QTL_Analysis_Fig1.ipynb**
- Plotting, analysis, and QTL mapping of melanization phenotypes

**Capsule_QTL_analysis_plotting_Fig_2_S2_Fig.ipynb**
- Analysis of capsule phenotypes and associated QTL analysis

**Temporal QTL mapping of AUC Figs 3 4 5 S3 S4 S5 S6 S9 Figs.ipynb**
- Temporal analysis, associated QTL mapping, and visualization of temporal growth phenotypes across temperatures and amphotericin B combinations

**SSK1_SSK2_RIC8_visualization_Fig6_S14_Fig.ipynb**
- Generates gene models of variants and their effects within candidate QTGs

**Cdx_Fludio_Crop_plot_Fig_7_8_S19_Fig.ipynb**
- Analysis and visualization of segregant fludioxonil phenotypes and H99 ric8 knockouts melanin phenotypes

**H2O2_QTL_Fig9.ipynb**
- QTL analysis of hydrogen peroxide growth phenotypes

**H2O2_plot_by_QTG_Fig10_S21_Fig.ipynb**
- Visualization of hydrogen peroxide data as a function of the three QTGs

### Scripts for supplemental figure generation

**Cdx-Allele-Frequency-S1-Fig.ipynb**
- Analysis of genome wide allele frequencies

**Cryptococcus_phenotypes_S7_S8_Figs.ipynb**
- Analysis of correlations across phenotypic data (capsule, melanin, thermal tolerance) of the mapping population

**Plot_growth_curves_candidate_QTG_knockouts_S10-13.ipynb**
- Generates figures showing growth curve data of knockouts at high temperatures with and without amphotericin B

**Median filtering knockouts S15 Fig.ipynb**
- Filtering and plotting of growth curve data collected on knockouts grown at high temperatures.

**Median filtering XL280 ssk1 knockouts S16 Fig.ipynb**
- Filtering of growth curve data collected on knockouts in the XL280 strain background

**Fine_mapped_QTL_Chr02_allele_freq_S17_Fig.ipynb**
- Analysis of bias allele frequencies on chromosome 2 in the fine-mapped progeny.

**Osmotic_QTL_analysis_Fig_S18.ipynb**
- QTL analysis of osmotic growth phenotypes

**Chromosome_12_SSK2_pleiotropic_QTL_S20_Fig.ipynb**
- Analysis of amphotericin B and hydrogen peroxide phenotypes

### Scripts for response to reviewers

**Effect_of_unisexual_vs_bisexual.ipynb**
- Explores bias in phenotypes based on type of cross used to generate segregants

**Replicate_analysis.ipynb**
- Analysis on reproducibility of phenotypic data