# Need Help?

## Technical support

Contact the Broken String Biosciences support team:

**Email:** [support@brokenstringbio.com](mailto:support@brokenstringbio.com)

---

## Common errors

| Error | Likely cause | Fix |
|-------|-------------|-----|
| Run fails immediately | Sample name / FASTQ prefix mismatch | Check manifest sample names match FASTQ prefixes exactly |
| Sample missing from report | Manifest or input error | Check **Workflow Warnings and Errors** in `report.html` |
| No homology-based nominations | Sense/antisense break positions not specified | Re-run with correct cut positions, or use discovery mode first |
| Very low break counts | Low library concentration | Check `*_qPCR_conc_pM_barchart.html` — optimal ≥ 0.2 pM |
| High duplicate rate | Library prep issue | Check FastQC `%Dups` — expected < 5% |

---

## Additional resources

| Resource | Link |
|----------|------|
| Full Analysis User Guide | [INDUCE-seq Analysis User Guide v2.0](https://www.brokenstringbio.com) |
| Technical Note #3 | How to Interpret INDUCE-seq Analysis Results *(link TBC)* |
| FAQs | *(link TBC)* |
| LatchBio documentation | [wiki.latch.bio](https://wiki.latch.bio) |

---

## Glossary

**Break** — A single DSB event detected by the INDUCE-seq pipeline. One read = one break.

**Break site** — A genomic location where one or more breaks are observed.

**Breakend** — The genomic coordinate and strand of an individual break.

**Breakcount** — Adjacent breaks that have been merged and counted into a single site.

**Condition** — The grouping label for samples that share the same treatment (used to label results in reports).

**Discovery mode** — Running the pipeline without specified sense/antisense break positions,
flagging any break within a guide-like sequence (±5 bp) as homology-based.

**Endogenous break** — A break arising from the cell's natural processes, not the editing treatment.
Most breaks detected are endogenous.

**Frequency-based nomination** — A break site nominated because its recurrency is unusually
high relative to background.

**Homology-based nomination** — A break site nominated because it overlaps a predicted cut
site at a genomic locus with sequence similarity to the guide.

**Nuclease mechanism** — The complete set of information describing the editing reagent:
nuclease type, guide sequence, PAM, and cut positions.

**Recurrency** — The number of breaks observed at the same break site. Higher recurrency
indicates a stronger signal relative to endogenous background.
