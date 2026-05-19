# gene2protein-

CYP2E1 Gene Assignment — README
Gene: CYP2E1
Ensembl ID: ENSG00000130649
Tissue: Liver
Function: Breaks down toxins and alcohol
Chromosome: 10 (plus strand, +) | Genome build: GRCh38 / hg38
Ensembl Database: AH119325 (via AnnotationHub, Bioconductor 3.23)

Files in This Submission
#FileDescription1Screenshot_2026-05-19_180402.pngIGV view of CYP2E1 (Task 1)2CYP2E1_gene_assignment.ipynbR notebook — transcripts, proteins & mapping (Tasks 2–4)3CYP2E1_protein_to_genome_map.tsvOutput map file — protein coords → genome (Task 4)4README.mdThis file

Task 1 — IGV View (Screenshot_2026-05-19_180402.png)
IGV was installed locally and loaded with the hg38 human reference genome.
CYP2E1 was navigated to using the gene name in the search bar.
What the screenshot shows:

Chromosome: 10
Coordinates visible: chr10:133,527 kb – 133,540 kb
Track: RefSeq All — showing the CYP2E1 transcript with exons (solid blue blocks) connected by introns (thin lines with directional arrows)
Strand: + (plus/forward strand — arrows point left to right)
Accession shown: OC105378575
The gene label CYP2E1 is visible at the centre of the view


Task 2 — List of Transcripts (Notebook Cell 4)
Fetched using transcripts(edb, filter = ~ gene_name == "CYP2E1") from ensembldb.
Total transcripts: 10
#Transcript ID1ENST000004631172ENST000005412613ENST000002529454ENST000004775005ENST000004183566ENST000004215867ENST000005410808ENST000004805589ENST0000036852010ENST00000469258

Task 3 — List of Proteins (Notebook Cell 5)
Fetched using proteins(edb, filter = ~ gene_name == "CYP2E1") from ensembldb.
Only transcripts with a valid CDS produce a protein — non-coding transcripts are automatically excluded.
Total proteins: 6
#Protein IDTranscript IDCDS OKProtein Length1ENSP00000440689ENST00000463117TRUE493 aa2ENSP00000437799ENST00000541261FALSE*86 aa3ENSP00000252945ENST00000252945TRUE493 aa (canonical)4ENSP00000397299ENST00000418356FALSE*306 aa5ENSP00000412754ENST00000421586FALSE*356 aa6ENSP00000444958ENST00000541080FALSE*43 aa

* cds_ok = FALSE means proteinToGenome() could not verify a CDS length match for that protein. Coordinates are still returned but should be interpreted with caution. A warning was printed in the notebook for these four proteins.


Task 4 — Protein-to-Genome Map (CYP2E1_protein_to_genome_map.tsv)
Generated using proteinToGenome() from ensembldb. Each row represents one exonic coding block where amino acid positions map to genomic coordinates.
File Details
PropertyValueFormatTab-separated (.tsv)Total rows37 (excluding header)Total proteins mapped6Genome buildGRCh38Chromosome10Strand+Genomic spanchr10:133,527,396 – 133,538,961
Column Descriptions
ColumnDescriptionseqnamesChromosome (10 for all CYP2E1 entries)startGenomic start coordinate of the exonic block (GRCh38)endGenomic end coordinate of the exonic block (GRCh38)widthLength of the block in base pairsstrandStrand of transcription (+ for CYP2E1)protein_idEnsembl protein ID (ENSP...)tx_idEnsembl transcript ID (ENST...)exon_idEnsembl exon ID (ENSE...)exon_rankOrder of the exon within the transcriptcds_okWhether CDS length matched the protein sequence (TRUE/FALSE)protein_startAmino acid start position mapped (always 1 — full protein mapped)protein_endAmino acid end position (equals total protein length in aa)
Exonic Blocks per Protein
Protein IDTranscript IDcds_okExonic BlocksProtein LengthENSP00000440689ENST00000463117TRUE9493 aaENSP00000437799ENST00000541261FALSE286 aaENSP00000252945ENST00000252945TRUE9493 aaENSP00000397299ENST00000418356FALSE7306 aaENSP00000412754ENST00000421586FALSE8356 aaENSP00000444958ENST00000541080FALSE243 aa

How to Re-run the Notebook

Open CYP2E1_gene_assignment.ipynb in Google Colab with an R kernel
Run all cells in order (Cell 1 through Cell 7)
The TSV output is saved to /content/compbioass/CYP2E1_protein_to_genome_map.tsv
Download via the Colab file browser (left panel → Files)

Dependencies (auto-installed in Cell 1)
rBiocManager::install("ensembldb")
BiocManager::install("AnnotationHub")
# Ensembl database loaded via:
ah  <- AnnotationHub()
edb <- ah[["AH119325"]]   # Ensembl 109, GRCh38

Key Notes

The two proteins with cds_ok = TRUE (ENSP00000440689 and ENSP00000252945) are the most reliable mappings — both are 493 amino acids, matching the canonical CYP2E1 protein.
The four proteins with cds_ok = FALSE are likely minor isoforms or truncated variants; their genomic coordinates are approximate.
CYP2E1 is on the plus (+) strand of chromosome 10, confirmed in both the IGV screenshot and the TSV file.
The notebook title says "ALDH2" in the markdown cell — this is a copy artefact from a classmate's notebook; all code and output is correctly for CYP2E1.


References

ensembldb coordinate mapping vignette: https://www.bioconductor.org/packages/release/bioc/vignettes/ensembldb/inst/doc/coordinate-mapping.html
Ensembl gene page: https://www.ensembl.org/Homo_sapiens/Gene/Summary?g=ENSG00000130649
IGV download: https://software.broadinstitute.org/software/igv/download
