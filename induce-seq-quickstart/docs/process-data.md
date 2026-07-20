# 1. Process Your Data

Before you can run the analysis, your raw sequencer output needs to be converted to FASTQ
format and uploaded to LatchBio.

---

## 1.1 Convert BCL to FASTQ

Raw sequencing output is stored in BCL format. You need to convert this into one FASTQ
file per sample using demultiplexing.

**What this produces:** one `*.fastq.gz` file per sample, with merged lanes.

!!! note "Demultiplexing"
    *[Reference your sequencer manufacturer's demultiplexing tool — e.g. Illumina's
    `bcl2fastq` or `BCL Convert`.]*

**Before moving on, confirm:**

- [ ] One FASTQ file exists per sample
- [ ] File names follow a consistent naming convention — you will use these to match
      samples in the manifest (sample names must match FASTQ prefix names exactly)

!!! warning "Name matching is critical"
    Sample names in your manifest must match FASTQ prefix names **exactly** — including
    capitalisation. A mismatch will cause the analysis run to fail.

---

## 1.2 Upload FASTQs to LatchBio

Sign in at [brokenstring.latch.bio](https://brokenstring.latch.bio) and navigate to the
**Your Analysis Workspace**.

### Option A — Upload from local storage *(straightforward, smaller datasets)*

1. Select **Data** from the left sidebar
2. Select **Create Folder** and name it for your experiment
3. Select your folder, then select **Upload** in the upper right
4. Drag your FASTQ files into the upload dialog, or select them manually
5. Select **Upload** and monitor progress via the **Uploaded Files** icon

### Option B — Mount cloud storage *(recommended for larger datasets)*

Connect an **Amazon S3** or **Google Cloud Platform (GCP)** bucket to LatchBio for faster
transfer and easier data management.

- S3: follow [LatchBio's Mount S3 Bucket guide](https://wiki.latch.bio/data/mount-s3-bucket)
- GCP: follow [LatchBio's Mount GCP Bucket guide](https://wiki.latch.bio/data/mount-gcp-bucket)

!!! tip "Folder organisation"
    Use a separate folder per experiment. A recommended structure:
    ```
    Experiment_1/
    ├── FASTQs/
    ├── Sample_manifest.csv
    ├── Nuclease_manifest.csv
    └── Results/
    ```

---

Once your FASTQs are uploaded and your QC data is to hand, continue to
[2. Run the Analysis](run-analysis.md).
