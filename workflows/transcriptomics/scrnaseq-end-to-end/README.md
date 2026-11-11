# Single-Cell RNA-Seq End-to-End Pipeline (STARsolo, AnnData, Seurat, SingleCellExperiment, MultiQC)

This workflow is a comprehensive, production-ready Galaxy translation of the [nf-core/scrnaseq](https://nf-co.re/scrnaseq) pipeline (version 4.2.0).

It executes the complete single-cell RNA-seq analytical lifecycle:
1. **Reference Sequence Filtering**: Ensures gene annotations strictly match the provided reference genome sequence.
2. **Read Quality Control**: Generates per-sample FastQC quality metrics.
3. **Alignment & Quantification**: Employs STARsolo for spliced alignment, cell barcode error correction (1MM multi-matching), UMI deduplication (1MM CR), and knee cell filtering (EmptyDrops / CellRanger2.2).
4. **AnnData Matrix Construction**: Transforms raw and filtered 10x MTX matrices into standardized AnnData (`.h5ad`) objects with Ensembl gene IDs and gene symbol annotations.
5. **Multi-Sample Concatenation**: Merges individual AnnData datasets into unified multi-sample datasets with unique barcode prefixes and optional samplesheet metadata joining.
6. **Downstream Format Export**: Converts merged AnnData into Seurat (`.seurat.rds`) and Bioconductor SingleCellExperiment (`.sce.rds`) objects.
7. **Quality Reporting**: Synthesizes read-level and mapping-level metrics into an interactive MultiQC HTML report.

## Inputs

- `reads`: A paired-end collection (`list:paired`) of FASTQ files (Read 1 = Barcode + UMI, Read 2 = cDNA).
- `fasta`: Reference genome sequence in FASTA format.
- `gtf`: Gene annotation file in GTF format.
- `barcode_whitelist`: (Optional) Text file of valid cell barcodes (e.g., 10x Genomics 737K V2 whitelist).
- `samplesheet`: (Optional) CSV/TSV table containing sample metadata to merge into the AnnData `obs` table.

## Outputs

- `Filtered Gene Expression Matrix`: Collection of filtered gene expression count matrices (Matrix Market format).
- `Filtered Cell Barcodes`: Collection of filtered cell barcode lists.
- `Filtered Gene Features`: Collection of gene feature TSVs.
- `Raw Gene Expression Matrix`: Collection of unfiltered gene expression count matrices.
- `Cell Barcodes`: Collection of all detected barcodes.
- `Gene Features`: Collection of gene features.
- `STARsolo Summary`: Detailed mapping, demultiplexing, and knee-filtering summary metrics.
- `FastQC Web Reports`: Collection of FastQC HTML quality reports.
- `Per-Sample Filtered AnnData Matrix`: Collection of per-sample AnnData H5AD files.
- `Combined Filtered AnnData Matrix`: Concatenated multi-sample AnnData H5AD object.
- `Combined Seurat RDS Object`: R RDS file containing Seurat object for downstream Seurat workflows.
- `Combined SingleCellExperiment RDS Object`: R RDS file containing SingleCellExperiment object for Bioconductor analysis.
- `MultiQC Quality Report`: Consolidated MultiQC HTML report.
