# 2. Run the Analysis

This step covers everything inside LatchBio: setting up your registry, building both
manifests, connecting your FASTQs, and launching the workflow.

---

## 2.1 Create a Registry Project

The Registry is where your experiment metadata lives. Organise manifests into projects —
one project per experiment is recommended.

1. Select **Data Registry** from the left sidebar
2. Select **+ New Project** in the upper left
3. Name the project after your experiment and select **Create**

---

## 2.2 Build your Nuclease Manifest

The nuclease manifest defines the editing reagent used in your experiment.

1. In **Data Registry**, hover over **Nuclease Manifest Template** under **Templates v2.0**
2. Select **···** → **Duplicate Table Schema** *(do not edit the template directly)*
3. Name the new manifest and assign it to your project
4. Select **Create**

**Fill in the required fields:**

| Field | Description | Example |
|-------|-------------|---------|
| `nuclease_mechanism` | Unique human-readable ID — you'll reference this in the sample manifest | `cas9_PDCD1` |
| `nuclease_type` | `cas9`, `cas12a`, or `custom` | `cas9` |
| `guide_sequence` | Spacer sequence **without** the PAM | `CACCTACCTAAGAACCATCC` |
| `pam` | Length + PAM format for your nuclease | `20-NGG` |

All other fields (sense/antisense break, mismatch threshold) are optional. See User Guide
Section 5.1 for a full column reference.

!!! tip "Few nucleases? Enter data manually"
    For one or two nuclease mechanisms, entering data directly in the workspace is faster
    than importing a CSV. For more, export the empty template, fill in Excel, and reimport
    via **Import → Import from File**.

!!! note "Placeholder"
    *[Short video or screenshots of nuclease manifest setup to be added here.]*

---

## 2.3 Build your Sample Manifest

The sample manifest links each sample to its nuclease mechanism and FASTQ files.

1. In **Data Registry**, hover over **Sample Manifest Template** under **Templates v2.0**
2. Select **···** → **Duplicate Table Schema**
3. Name the manifest and assign it to your project
4. Select **Create**

**Key fields:**

| Field | Description | Example |
|-------|-------------|---------|
| `sample` | Must match the FASTQ prefix **exactly** | `Cas9_PDCD1_24h_rep1` |
| `nuclease_mechanism` | Must match the value in your nuclease manifest | `cas9_PDCD1` |
| `condition` | Groups replicates — also labels samples in reports | `Cas9_PDCD1_24h` |
| `control` | Enter `control` for untreated samples; for treated samples enter the matching control's condition value | `control_Cas9` |

Leave `fastq_1`, `fastq_2`, and `breakends` blank — these are populated in the next step.

!!! warning
    No spaces or periods in sample names. Sample names must match FASTQ prefixes exactly —
    a mismatch will cause the run to fail.

!!! tip "Multiple samples? Use CSV import"
    Export the empty manifest as CSV (**Export → Export View as CSV**), fill it in Excel,
    then reimport via **Import → Import from File**. This is faster than manual entry for
    more than a few samples.

!!! note "Placeholder"
    *[Short video or screenshots of sample manifest setup to be added here.]*

---

## 2.4 Connect your FASTQs

Link each sample to its FASTQ file(s) using bulk import — this is the recommended method
for most datasets.

1. In **Data Registry**, navigate to your sample manifest
2. Select **Import → Bulk Import Sequencing Data**
3. Navigate to your FASTQ folder and select the folder (or hold Shift to select individual files)
4. Select **Modify Name Parsing → Specify Manually** to trim file names to match your sample names
5. Turn on **Left Join** to match only FASTQs with sample names in your manifest
6. Select `fastq_1` as the **Target Column for Read 1** (and `fastq_2` for Read 2 if paired-end)
7. Select **Import**

!!! tip
    LatchBio splits file names by `_`, `-`, and `.` separators. Use the name parsing tool
    to select how many components to keep so names match your manifest exactly.

---

## 2.5 Launch the Workflow

1. Select **Workflows** from the left sidebar, then select **INDUCE-seq**
2. Under **Sample Manifest Input**: select **Registry Sample Manifest → Import Rows from Registry**,
   navigate to your manifest, select your samples, confirm column mapping, and select **Import**
3. Under **Nuclease Manifest Input**: repeat the same steps for your nuclease manifest
4. Select your **sequencing platform**
5. Select a **reference genome**:
    - Standard: `hg19`, `hg38`, or `t2t`
    - Custom genome: upload a BWA-indexed genome, FASTA, and chromosome sizes file to LatchBio
      first (see User Guide Section 8.1 for full custom genome requirements)
6. Select an **output folder**
7. Enter an **execution name** (alphanumeric, underscores, and hyphens only)
8. Select **Launch Workflow**

!!! note "Placeholder"
    *[Short video of workflow launch to be added here.]*

---

## 2.6 Monitor your run

Go to **Workflows → All Executions** and double-click your execution name to track progress.

**Execution statuses:**

| Status | Meaning |
|--------|---------|
| Queued | Awaiting compute resources |
| Initializing | Starting up |
| Building | Preparing the pipeline |
| Running | In progress |
| Succeeded | Completed without uncaught errors |
| Failed | Could not complete — contact [support@brokenstringbio.com](mailto:support@brokenstringbio.com) |

!!! warning "Succeeded ≠ error-free inputs"
    A successful execution means no uncaught pipeline errors. Input manifest errors
    (e.g. mismatched sample names) will appear in the **Workflow Warnings and Errors**
    section of your HTML report — always check this first.

---

Once the execution shows **Succeeded**, continue to [3. Explore Your Results](explore-results.md).
