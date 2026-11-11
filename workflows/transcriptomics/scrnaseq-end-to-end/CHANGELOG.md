# Changelog

All notable changes to this workflow will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this workflow adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-11-11

### Added
- Complete end-to-end Galaxy translation of `nf-core/scrnaseq` pipeline (version 4.2.0).
- Modular pipeline stages:
  - Reference genome preparation and GTF sequence filtering (`gtf-gene-filter` UDT).
  - FastQC read quality control.
  - STARsolo alignment, cell barcode demultiplexing, error correction, and gene quantification.
  - 10x MTX to per-sample AnnData H5AD conversion (`mtx-to-h5ad` UDT).
  - Multi-sample AnnData concatenation and metadata joining (`concat-h5ad` UDT).
  - Multi-format downstream export to Seurat RDS and SingleCellExperiment RDS (`anndatar-convert` UDT).
  - MultiQC reporting combining FastQC and STARsolo metrics.
- Comprehensive test assertions across all output data types and formats.
