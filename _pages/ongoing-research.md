---
layout: archive
title: "Ongoing Research Works"
permalink: /ongoing-research/
author_profile: true
---

{% include base_path %}

Current research projects with Elite Research Lab PLC and independent research work in trustworthy AI, multimodal learning, biomedical data quality, and retrieval-augmented generation.

## Elite Research Lab PLC

### AI Tutor for NCTB Educational Content

Developing the data foundation for a curriculum-grounded, multimodal Retrieval-Augmented Generation (RAG) tutor for Bangladeshi school students. The system is intended to cover Classes 1–10 and answer questions from official NCTB textbooks in Bengali, Arabic, and English while prioritizing factual fidelity to the source curriculum.

The project began with an audit of the third-party NCTB-SchoolText corpus, covering **1,535 chapters and 58,872 text chunks**. The audit identified OCR corruption, missing content, malformed records, duplication, and chapter-boundary errors. Because the original PDFs used vector-outlined text, direct extraction was not reliable; the corpus is being re-converted from **132 official NCTB PDFs** using rasterization, validated OCR, independent chapter segmentation, and resumable JSONL processing. The current pipeline uses Google Drive OCR for non-generative transcription and preserves section metadata for downstream retrieval.

### PCOS Dataset Quality and Integrity Audit

Auditing publicly available PCOS datasets across tabular, ultrasound-image, and detection-annotation formats. The work evaluates provenance, label definitions, missing and implausible values, formula artifacts, leakage, duplication, cross-split overlap, image metadata shortcuts, annotation consistency, and licensing or access limitations.

The audit has already identified criterion leakage, synthetic or unusable datasets, duplicate image collections, inconsistent annotation schemas, and near-perfect image results driven by acquisition metadata rather than morphology. It also establishes a reusable verification protocol so that PCOS models can be evaluated on data that is clinically and technically trustworthy.

### Multimodal PCOS Detection Pipeline

Designing a multimodal deep-learning pipeline that combines information from the **same patient** across clinical/tabular data and ovarian ultrasound images for more effective PCOS detection. The intended architecture supports separate modality-specific branches, calibrated fusion, and evaluation under full and partial information.

The current work is verification-first: the candidate dataset claims patient-level linkage between ultrasound images, clinical records, and manually determined diagnosis. Before model training, patient IDs, diagnostic labels, image-folder labels, feature quality, duplication, leakage, and cross-subset consistency must be independently verified. This prevents a seemingly multimodal model from being trained on mismatched or shortcut-driven data.

## Independent Research

### MechRAG: Interpreting Drug Side Effects

MechRAG is a retrieval-augmented explanation system that connects drug targets to likely tissue-level side effects using biological evidence. The pipeline integrates DrugBank and SIDER with GTEx tissue expression, STRING protein interactions, and KEGG pathway data for **859 real drugs**.

Three evidence configurations were evaluated: gene expression alone, expression plus interaction partners, and expression plus pathway information. The combined evidence improved top-three tissue prediction from **41.7% to 46.6%**, significantly outperforming random chance. A locally hosted language model then generated evidence-grounded explanations, while an automated checker verified that explanations did not introduce unsupported genes, tissues, or pathways. After iterative checker fixes, **819 of 830 explanations (98.7%) were clean**, with additional cases correctly abstaining rather than guessing.

## Research Themes

**Trustworthy AI:** Dataset auditing, leakage detection, provenance verification, and evidence-grounded generation.  

**Multimodal learning:** Combining clinical, image, and structured evidence while preserving patient-level linkage and calibrated evaluation.  

**Retrieval-Augmented Generation:** Building systems that answer from authoritative source material and expose uncertainty instead of fabricating content.  

**Biomedical AI:** Reproducible analysis of PCOS diagnosis and mechanistic interpretation of drug side effects.
