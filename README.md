# gene2protein-

## CYP2E1 Gene Assignment — README

| Property | Value |
|----------|-------|
| Gene | CYP2E1 |
| Ensembl ID | ENSG00000130649 |
| Tissue | Liver |
| Function | Breaks down toxins and alcohol |
| Chromosome | 10 (plus strand, +) |
| Genome build | GRCh38 / hg38 |
| Ensembl Database | AH119325 (via AnnotationHub, Bioconductor 3.23) |

## Files in This Submission

| # | File | Description |
|----|------|-------------|
| 1 | Screenshot_2026-05-19_180402.png | IGV view of CYP2E1 (Task 1) |
| 2 | CYP2E1_gene_assignment.ipynb | R notebook — transcripts, proteins & mapping (Tasks 2–4) |
| 3 | CYP2E1_protein_to_genome_map.tsv | Output file with protein-to-genome mappings |

## Task 1 — IGV View (Screenshot_2026-05-19_180402.png)

IGV was installed locally and loaded with the hg38 human reference genome.
CYP2E1 was navigated to using the gene name in the search bar.

### What the screenshot shows:

- **Chromosome**: 10
- **Coordinates visible**: chr10:133,527 kb – 133,540 kb
- **Track**: RefSeq All — showing the CYP2E1 transcript with exons (solid blue blocks) connected by introns (thin lines with directional arrows)
- **Strand**: + (plus/forward strand — arrows point left to right)
- **Accession shown**: OC105378575
- **Gene label**: CYP2E1 is visible at the centre of the view

## Task 2 — List of Transcripts (Notebook Cell 4)

Fetched using `transcripts(edb, filter = ~ gene_name == "CYP2E1")` from ensembldb.

**Total transcripts: 10**

| # | Transcript ID |
|----|---------------|
| 1 | ENST00000463117 |
| 2 | ENST00000541261 |
| 3 | ENST00000252945 |
| 4 | ENST00000477500 |
| 5 | ENST00000418356 |
| 6 | ENST00000421586 |
| 7 | ENST00000541080 |
| 8 | ENST00000480558 |
| 9 | ENST00000368520 |
| 10 | ENST00000469258 |

## Task 3 — List of Proteins (Notebook Cell 5)

Fetched using `proteins(edb, filter = ~ gene_name == "CYP2E1")` from ensembldb.

Only transcripts with a valid CDS produce a protein — non-coding transcripts are automatically excluded.

**Total proteins: 6**

| # | Protein ID | Transcript ID | CDS OK | Protein Length |
|----|-----------|---|--------|----------------|
| 1 | ENSP00000440689 | ENST00000463117 | TRUE | 493 aa |
| 2 | ENSP00000437799 | ENST00000541261 | FALSE* | 86 aa |
| 3 | ENSP00000252945 | ENST00000252945 | TRUE | 493 aa (canonical) |
| 4 | ENSP00000397299 | ENST00000477500 | TRUE | 493 aa |
| 5 | ENSP00000413902 | ENST00000418356 | FALSE* | 248 aa |
| 6 | ENSP00000421863 | ENST00000421586 | FALSE* | 246 aa |

**Note**: `cds_ok = FALSE` means `proteinToGenome()` could not verify a CDS length match for that protein. Coordinates are still returned but should be interpreted with caution. A warning was printed in the notebook.

## Task 4 — Protein-to-Genome Map (CYP2E1_protein_to_genome_map.tsv)

Generated using `proteinToGenome()` from ensembldb. Each row represents one exonic coding block where amino acid positions map to genomic coordinates.

### File Details

| Property | Value |
|----------|-------|
| Format | Tab-separated (.tsv) |
| Total rows | 37 (excluding header) |
| Total proteins mapped | 6 |
| Genome build | GRCh38 |
| Chromosome | 10 |
| Strand | + |
| Genomic span | chr10:133,527,396 – 133,538,961 |

### Column Descriptions

| Column | Description |
|--------|-------------|
| seqnames | Chromosome (10 for all CYP2E1 entries) |
| start | Genomic start coordinate of the exonic block (GRCh38) |
| end | Genomic end coordinate of the exonic block (GRCh38) |
| width | Length of the block in base pairs |
| strand | Strand orientation (+ for all CYP2E1) |
| protein_id | Ensembl protein identifier |
| tx_id | Ensembl transcript identifier |
| exon_id | Exon identifier |
| exon_rank | Rank of the exon within the transcript |
| seq_name | Chromosome name |
| protein_start | Start position in the protein (amino acid) |
| protein_end | End position in the protein (amino acid) |

### Exonic Blocks per Protein

| Protein ID | Transcript ID | CDS OK | Exonic Blocks | Protein Length |
|-----------|---------------|--------|----------------|----------------|
| ENSP00000440689 | ENST00000463117 | TRUE | 9 | 493 aa |
| ENSP00000437799 | ENST00000541261 | FALSE | 2 | 86 aa |
| ENSP00000252945 | ENST00000252945 | TRUE | 9 | 493 aa |
| ENSP00000397299 | ENST00000477500 | TRUE | 9 | 493 aa |
| ENSP00000413902 | ENST00000418356 | FALSE | 8 | 248 aa |
| ENSP00000421863 | ENST00000421586 | FALSE | 8 | 246 aa |

## How to Re-run the Notebook

1. Open `CYP2E1_gene_assignment.ipynb` in Google Colab with an R kernel
2. Run all cells in order (Cell 1 through Cell 7)
3. The TSV output is saved to `/content/compbioass/CYP2E1_protein_to_genome_map.tsv`
4. Download via the Colab file browser (left panel → Files)

## Dependencies (auto-installed in Cell 1)

```r
BiocManager::install("ensembldb")
BiocManager::install("AnnotationHub")

# Ensembl database loaded via:
ah  <- AnnotationHub()
edb <- ah[["AH119325"]]   # Ensembl 109, GRCh38
```

## Key Notes

- The two proteins with `cds_ok = TRUE` (ENSP00000440689 and ENSP00000252945) are the most reliable mappings — both are 493 amino acids, matching the canonical CYP2E1 protein.
- The four proteins with `cds_ok = FALSE` are likely minor isoforms or truncated variants; their genomic coordinates are approximate.
- CYP2E1 is on the plus (+) strand of chromosome 10, confirmed in both the IGV screenshot and the TSV file.
- The notebook title says "ALDH2" in the markdown cell — this is a copy artifact from a classmate's notebook; all code and output is correctly for CYP2E1.

## References

- [ensembldb coordinate mapping vignette](https://www.bioconductor.org/packages/release/bioc/vignettes/ensembldb/inst/doc/coordinate-mapping.html)
- [Ensembl gene page](https://www.ensembl.org/Homo_sapiens/Gene/Summary?g=ENSG00000130649)
- [IGV download](https://software.broadinstitute.org/software/igv/download)
