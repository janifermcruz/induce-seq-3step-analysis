# Before You Begin

Use this checklist to confirm you have everything needed before launching an analysis run.
All items are required unless marked optional.

---

## Sample inputs

- [ ] **Sample sheet** — the `sample_sheet.csv` used during the sequencing run
- [ ] **FASTQ files** — one per sample, output from BCL conversion (see [Process Your Data](process-data.md))
- [ ] **Sequencer QC metrics** — Q30 score and % Pass Filter (%PF) from your sequencing run report
- [ ] **Assay QC data** *(optional but highly recommended)* — gDNA yield (ng), library yield (ng), and library concentration (pM) from Qubit and qPCR

!!! tip "Why assay QC matters"
    Supplying gDNA yield, library yield, and qPCR concentration (pM) unlocks the lab metrics
    QC plots in your results. A library concentration ≥ 0.2 pM is optimal for sufficient
    sensitivity. These fields are optional but help you catch upstream issues early.

---

## Nuclease inputs

- [ ] **Guide sequence** — the spacer sequence used to target your region of interest, *without* the PAM
- [ ] **PAM sequence** — in the correct format for your nuclease type:
    - Cas9: `20-NGG` (replace 3' PAM end with NGG)
    - Cas12a: `TTTV-21` (replace 5' PAM end with TTTV)
    - Custom: `X-PAM` or `PAM-X` depending on PAM position

!!! note "First time running a custom nuclease?"
    Leave the `sense_break` and `antisense_break` fields blank to run in **discovery mode**.
    This flags any break within a guide-like sequence (±5 bp) as homology-based, letting you
    identify the cutting pattern empirically before specifying exact cut positions in a second run.
    See User Guide Section 5.1 for details.

---

## LatchBio access

- [ ] You have a LatchBio account — sign in at [brokenstring.latch.bio/login](https://brokenstring.latch.bio/login)
    or sign up at [brokenstring.latch.bio/signup](https://brokenstring.latch.bio/signup)
- [ ] You have received your **BSB INDUCE-seq Analysis Workspace invite link** from Broken String Biosciences
    *(links are valid for 7 days and can be shared with collaborators)*
- [ ] Your workspace has sufficient **LatchBio credits** for a compute run

---

When all boxes are checked, continue to [1. Process Your Data](process-data.md).
