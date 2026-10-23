# Judging “AI or Human” Under Uncertainty

## Reproducibility materials for TikTok AI-provenance judgments

This repository contains de-identified supplementary materials and R code for a study of how TikTok users publicly attribute video provenance to AI, express uncertainty, make non-AI provenance claims, provide reasons, and receive interactional responses.

The repository documents the current revised manuscript's measurement and audit chain: human coding, model-assisted high-recall retrieval, second-coder reliability, rule-based adjudication, negative-audit uncertainty, within-video core comparisons, conditional clustering diagnostics, language/sample reconciliation, and interaction-model sensitivity checks.

## Study at a glance

The source archive contained **57,931 videos** and **2,737,540 parsed comments**. The frozen V3.5.5 main-analysis/prediction cache contains **1,110,044 comments**. The final human-confirmed AI-provenance corpus contains **1,317 comments**.

Machine learning was used as a **candidate-retrieval device**, not as the final substantive label. In grouped out-of-fold evaluation, the model+rule union achieved precision = **0.629**, recall = **0.993**, and F1 = **0.770**. After full review of new candidates and a stratified audit of predicted negatives, the end-to-end retrieval-recall point estimate was approximately **0.947**. Because only two AI positives were found in the 2,000-comment negative audit, the repository also reports stratum-specific uncertainty rather than treating 0.947 as exact.

A later independent reliability audit focused on 56 comments that had previously entered the core A/C comparison after a single final review. The second-coder results showed:
- stance agreement = **85.7%**, Cohen’s κ = **0.625**;
- A/C-specific agreement = **87.3%**, κ = **0.658**;
- explicit-reason agreement = **96.4%**, κ = **0.837**.

After rule-based adjudication of 10 disagreements, the core comparison contains **215 comments from 48 videos**:
- A (AI assertion): n = **122**, explicit reason n = **17**;
- C (non-AI provenance claim): n = **93**, explicit reason n = **24**.

The updated within-video fixed-effect difference is β = **0.135**, cluster SE = **0.065**, 95% CI **[0.005, 0.265]**, p = **0.042**. The video-equal estimate is **0.153** (p = **0.044**), the wild-cluster bootstrap p-value is **0.047**, and leave-one-video-out estimates range from approximately **0.114 to 0.160**. These checks support a positive direction while also showing that conventional significance is not invariant to every reasonable perturbation.

## Important interpretation boundaries

The repository supports analysis of **observable platform behavior**. It does not directly measure attention, cognitive effort, subjective uncertainty, exposure to prior comments, evidence search, or judgment accuracy. Source-monitoring, epistemic-vigilance, heuristic-systematic processing, and social-authentication theories are therefore used as interpretive frameworks rather than directly observed mechanisms.

Likewise:
- likes/replies are **interactional uptake**, not belief or persuasion;
- within-video concentration is not contagion;
- same-video co-occurrence is not a direct reply relation;
- AI provenance is not factual falsity;
- a non-AI provenance claim is not automatically a correction or repair action.

## Repository structure

```text
01_codebook/
02_code/
03_retrieval_audit/
04_core_reliability/
05_core_analysis/
06_negative_audit/
07_clustering/
08_language_and_sample_audit/
09_interaction_sensitivity/
docs/
```

See `docs/SUPPLEMENTARY_MATERIALS_INDEX.md` for a file-by-file map.

## Internal label terminology

The frozen code and some frozen output files use the internal label `counter_authentication`. The revised manuscript uses the more conservative descriptive term **non-AI provenance claim** for category C. The internal computational label is retained in frozen files to preserve reproducibility.

## Retrieval pipeline

The frozen `AI_Provenance_AllInOne_V3_5_5.R` pipeline implements:

1. loading the existing parsed/prelabelled comment cache;
2. AI-specific human-gold construction;
3. grouped out-of-fold high-recall retrieval;
4. word 1–2 gram, character 3–5 gram, and structured lexical features;
5. elastic-net logistic retrieval;
6. union of model retrieval and explicit AI rules;
7. human review of all newly retrieved candidates;
8. stratified human audit of predicted negatives;
9. construction of the human-confirmed AI-provenance corpus;
10. stance/reason, conditional permutation, and interaction analyses.

The main script requires the locally held parsed/prelabelled cache and human-review files. Raw platform data are not included in this public repository.

### R packages used

`data.table`, `quanteda`, `glmnet`, `Matrix`, `stringi`, `stringr`, `lubridate`, `fixest`, `ggplot2`, `broom`, and `scales`.

## Language/count reconciliation

A later diagnostic script that applied `trimws()` classified four raw language values containing `en\n` as English, producing 1,110,048 normalized English rows. The frozen V3.5.5 prediction cache contains 1,110,044 rows. Reconciliation found no duplicated comment keys and exactly four normalized-English records absent from the frozen prediction cache; those four records were not provenance-relevant or AI challenges.

Accordingly, **1,110,044 remains the canonical frozen V3.5.5 analysis/prediction count**. The normalized audit is retained to document how the four-row discrepancy arose.

## Interaction-model sensitivity

The repository includes the frozen V3.5.5 interaction coefficients, retained video fixed-effect counts from the normalized-cache audit, and sensitivity checks after removing the top 0.1% and 1% of interaction counts. The trimming checks did not reverse the direction of the AI-challenge coefficient.

The normalized-cache audit is kept separate from the frozen V3.5.5 model outputs because of the four-row language-normalization difference described above.

## Data availability and privacy

Raw TikTok comments, usernames, account IDs, comment/video IDs, direct links, and verbatim 56-comment recheck materials are intentionally excluded. Public process files use anonymous review IDs and anonymous video-cluster IDs.

See `docs/DATA_AVAILABILITY_AND_PRIVACY.md`.

## Versioning

The post-review 56-comment reliability audit updated the core A/C comparison from 216 to 215 comments. Full-corpus permutation and interaction results remain the frozen V3.5.5 outputs because the complete raw/cache data are not redistributed here.

See `docs/VERSIONING_NOTE.md`.

## Citation

Add the final article citation after the manuscript has a stable publication record. Until then, cite this repository by repository title, authors, GitHub URL, and version/access date.

## License

No license file is included. Choose a code/data/documentation license appropriate to the manuscript, source-data permissions, and institutional requirements before making the repository public.
