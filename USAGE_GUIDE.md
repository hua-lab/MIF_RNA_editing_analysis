# Step-by-Step Usage Guide

This guide walks you through reproducing the full organelle RNA sequencing analysis pipeline described in:

**Hua, Z. et al. (2026)** _F-box protein-mediated turnover of multiple organellar RNA-editing factor 2 coordinates seed germination and plastid signaling.

---

## 📁 1. Clone the Repository
```bash
git clone https://github.com/hua-lab/MIF_RNA_editing_analysis.git
cd MIF_RNA_editing_analysis

```

## ⚙️ 2. Run Method S1 – Demultiplex and Strand-Correct FASTQ Files
```bash
mv *.* ./raw_FASTQs
cd raw_FASTQs
gunzip *.gz
perl filter_barcoded_fastq_seqs.pl
```

## 🧬 3. Run Method S2 – Align Strand-Corrected Reads to the Pseudo-Genome
```bash
chmod +x ./run_minimap_alignments.sh
./run_minimap_alignments.sh
```

## 🧪 4. Run Method S3 – Extract and Quantify Intron-Retaining Transcripts
```bash
# First, move the necessary files into the minimap_alignments folder:

mv count_groupII_inserts_and_extract.py ./minimap_alignments
mv ndhB_intron.fasta ./minimap_alignments
mv local_align_inserts_vs_intron_blast.pl ./minimap_alignments
cd minimap_alignments

# Then, set up and activate a virtual Python environment:

python3 -m venv venv
source venv/bin/activate
pip install biopython pandas

# Now run the script:

python count_groupII_inserts_and_extract.py

# Deactivate the environment when done

deactivate

```

## 🔍 5. Run Method S4 – BLAST Analysis of Unspliced Reads
```bash
perl local_align_inserts_vs_intron_blast.pl
```

## ✅ Outputs

`minimap_alignments/`: Contains BAM and BAI files for manual inspection of C-to-U RNA editing using IGV  
`ndhB_groupII_insertion_count_chr1-3.tsv`: Summary table of intron-retention frequencies by sample and genotype  
`insert_fastas/`: Per-sample FASTA files containing unspliced reads with Group II intron insertions  
`merged_fastas/`: Genotype-wise merged FASTA files for downstream alignment or BLAST  
`ndhB_insert_vs_intron_blast.tsv`: Summary of BLASTN alignments between unspliced inserts and the reference intron  


