# MIF_RNA_editing_analysis

Bioinformatics pipeline and sequencing data supporting the study:  
**Hua, Z.*, et al. (2026).** *F-box protein-mediated turnover of multiple organellar RNA-editing factor 2 coordinates seed germination and plastid signaling*.

This repository contains raw sequencing data and custom scripts used for the analysis of RNA editing and intron retention in chloroplast transcripts using Oxford Nanopore Target-Indexed PCR (TIP) sequencing.

In this study, increased RNA editing errors were observed in MORF2-interacting F-box overexpression (MIF-OE) lines following dexamethasone-induced MIF expression compared to wild-type (WT) controls, whereas no significant differences in intron retention were detected across genotypes.

---

## 📁 Contents

### Dataset & Reference Sequences  
- `raw_FASTQs/` — Raw FASTQ files from nanopore barcoded amplicon sequencing  
- `pseudo_genome_ndhBD.fa` — Synthetic pseudo-genome reference used for alignment  
- `ndhB_intron.fa` — Reference sequence of the Group II intron in *ndhB*

### Scripts  
- `filter_barcoded_fastq_seqs.pl` — Barcode filtering and strand correction  
- `run_minimap_alignments.sh` — Alignment using `minimap2` and processing with `samtools`  
- `count_groupII_inserts_and_extract.py` — Detection of unspliced reads and FASTA export  
- `local_align_inserts_vs_intron_blast.pl` — Local alignment of unspliced reads using `BLASTN`

### Example Outputs  
- `minimap_alignments/` — BAM/BAI files from alignment  
- `insert_fastas/` and `merged_fastas/` — FASTA files of unspliced reads  
- `ndhB_groupII_insertion_count_chr1-3.tsv` — Summary of intron retention frequencies  
- `ndhB_insert_vs_intron_blast.tsv` — BLASTN alignment summary of unspliced reads  

### Documentation  
- `USAGE_GUIDE.md` — Step-by-step instructions for reproducing the analysis pipeline  

---

## 🧪 System Requirements & Dependencies

**Tested on:** macOS (ARM64)

### Required software  
- **Perl** ≥ 5.40.1 with **BioPerl** ≥ 1.7.8  
- **Python** ≥ 3.11 with:
  - `biopython` ≥ 1.81  
  - `pandas` ≥ 2.2.2  
- **minimap2** ≥ v2.29  
- **samtools** ≥ v1.21  
- **NCBI BLAST+** ≥ v2.16.0  

---

## 📊 Data Availability

Raw Oxford Nanopore TIP-sequencing data are also available in the NCBI Sequence Read Archive (SRA) under BioProject accession **PRJNA1456570**.

---

## 📬 Contact

**Zhihua Hua, Ph.D.**  
Associate Professor  
Department of Environmental & Plant Biology  
Ohio University  
📧 hua@ohio.edu  
🔗 ORCID: https://orcid.org/0000-0003-1177-1612
