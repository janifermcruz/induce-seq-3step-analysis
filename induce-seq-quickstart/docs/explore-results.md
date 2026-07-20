# 3. Explore Your Results

Your results are available in the **Data** tab under the output folder you selected at launch.
Start with the HTML report — it is the fastest way to assess your run.

---

## 3.1 Open the HTML Report

Navigate to your output folder and open `Primary_Outputs/report.html`.

The report contains:

- **Nomination list** — ranked candidate off-target and on-target break sites
- **Mismatch plot** — break sites intersected with in silico guide homology predictions
- **Breaksite plots** — two per condition (highest recurrency site + fewest mismatches to guide)
- **QC plots** — sequencing and library quality metrics
- **Workflow Warnings and Errors** — check this table first if results look unexpected

!!! tip "Start here if something looks wrong"
    The **Workflow Warnings and Errors** table captures manifest mismatches, low read counts,
    and samples excluded from the run. If a sample is missing from your results, the reason
    will be listed here.

!!! note "Placeholder"
    *[Screenshot of example report.html to be added here.]*

---

## 3.2 Review the Nomination List

The nomination list (`Primary_Outputs/Nomination_Lists/*_combined_nominations.tsv`) ranks
break sites most likely to be induced by your editing treatment.

Sites are nominated on two rationales:

**Frequency-based** — sites with unusually high recurrency relative to the background break
landscape. Sites are sorted by absolute break count; when the number of sites in a recurrency
class exceeds 10, lower-recurrency classes are dropped.

**Homology-based** — sites that overlap with the expected cut position of your nuclease at
genomic locations with sequence similarity to your guide sequence (up to 6 mismatches by default).

**Key columns to review first:**

| Column | What to look at |
|--------|----------------|
| `count` | Total breaks at the site — higher = stronger signal |
| `rationale` | `frequency-based`, `homology-based`, or both |
| `guide_name_mismatches` | Number of mismatches to the guide — fewer = higher confidence |
| `break_site_probability_score` | % probability the site is treatment-induced, not endogenous. A score ≥ 80% is a suggested threshold for true positives |
| `reproducibility_count` | How many replicates show the site (e.g. `2/3`) |
| `normalized_sample_to_control_ratio` | Treated vs control enrichment — higher = more induced |

!!! note "Placeholder"
    *[Screenshot of example nomination list to be added here.]*

---

## 3.3 Check the QC Plots

QC plots are in the `QC/` folder. Key thresholds:

| Metric | What to check | Optimal value |
|--------|--------------|---------------|
| gDNA yield | `*_gDNA_yield_ng_barchart.html` | ≥ 100 ng |
| Library concentration | `*_qPCR_conc_pM_barchart.html` | ≥ 0.2 pM |
| Read loss | `*_read_loss.html` | > 75% primary reads (orange); minimal unmapped (green) |
| Duplicate rate | FastQC General Statistics `%Dups` | < 5% |
| Phred score (trimmed) | FastQC Sequence Quality Histogram | > 30 across all positions |

---

## 3.4 Inspect Breaksite Plots

Breaksite plots (`Primary_Outputs/Break_Site_Plots/`) show the distribution and frequency
of breaks at per-base resolution for each nominated site.

- **Red bars** — breaks on the positive (+) strand
- **Blue bars** — breaks on the negative (−) strand
- Edited sample and control are shown on the same scale for direct comparison
- Hover over bars for exact break counts and position details

If you ran in **discovery mode** (no sense/antisense break values set), use these plots to
identify the empirical cutting positions. You can then enter these values in the nuclease
manifest and relaunch for more precise homology-based nominations.

!!! note "Placeholder"
    *[Screenshot or short video of breaksite plot interaction to be added here.]*

---

## 3.5 View in IGV

Break-level files can be loaded directly into
**[Integrative Genomics Viewer (IGV)](https://igv.org)** for read-level visual inspection.

**Files to load:**

| File | Location | What it shows |
|------|----------|---------------|
| `*_breakends.bed.gz` | `Secondary_Outputs/Breakends/` | Individual break positions and strand |
| `*_breakcount.bed.gz` | `Primary_Outputs/Breakcounts/` | Merged and counted break sites |
| `*.bam` | `Secondary_Outputs/Sequence_Mapping/` | Mapped reads (mapQ ≥ 30, primary only) |

**To load in IGV:**

1. Open IGV and select the same reference genome used in your analysis run
2. Select **File → Load from File** and open your `.bed.gz` or `.bam` file
3. Navigate to a nominated break site from your nomination list to inspect at read level

!!! tip
    You can load multiple samples at once and examine any genomic region of interest. 

!!! note "Placeholder"
    *[Short video of IGV walkthrough to be added here.]*

---

## You're done

You've completed the full INDUCE-seq Analysis workflow — from sequencing run to IGV.

For deeper interpretation of your results, see
[Technical Note #3: How to Interpret INDUCE-seq Analysis Results]().

Questions? Contact [support@brokenstringbio.com](mailto:support@brokenstringbio.com).
