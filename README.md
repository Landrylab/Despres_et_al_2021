# Despres_et_al_2021
Notebooks for data analysis and figure generation of Despres et al 2021, "Asymmetrical dose-responses shape the evolutionary trade-off between antifungal resistance and nutrient use"

The notebooks for the Deep Mutationnal Scanning (DMS) data analysis and growth curves are listed here. The main analysis steps for sequencing data are also explained here (as well as in the methods section of the manuscript). Most bioinformatics was performed in Jupyter Notebooks using Python 3.7.9.

## Python Packages
 - pandas 1.2.1
 - numpy 1.19.2
 - matplotlib 3.3.2
 - scipy 1.5.2
 - seaborn 0.11.1

## Programs required:
 - FastQC 0.11.5
 - Trimmomatic 0.39 (make sure to change the path in the notebooks to the one appropriate for your environment)
 - pandaseq 2.11
 - vsearch 2.7.1
 - needle (as part of EMBOSS 6.6.0.0)

## DMS Notebooks included in the repository:
 - DMS_analysis: details the pipeline to go from the MiSEQ fastq file to relative abudances of each FCY1 codon level variant at each timepoints
 - Fold_change: details the data analysis steps to go from codon level relative abundance to amino acid level log2 fold-change 
 - Pymol_analysis: integrates the FCY1 FoldX data and other protein level information from various database in to the main DataFrame
 - Heatmaps: main notebook used to generate figures and perform statistical analysis
 - Predict ajdacent sequence

## Growth curve analysis notebooks included in the repository:





## DMS_analysis

This notebook processes the fastq files and performs the following operations:
1. Assess reads quality using FastQC
2. Select reads with correct length and crop the 3-prime end to remove low confidence bases
3. Demultiplex the libraries that were combined using the plate [RC-PCR library](https://pubmed.ncbi.nlm.nih.gov/27107012/) construction workflow

Then, for each library

4. Merge R1 and R2 using panda-seq
5. Trim amplicons to remove adapter and barcode regions
6. Aggregate identical reads together
7. Align reads on the appropriate FCY1 cds reference
8. Parse alignment to detect mutations
9. Filter alignments and determine the effects of the mutations on the FCY1 cds at the codon level
10. Sum variant abundances and calulate relative abundance of each FCY1 cds variant, and save as csv for each library

