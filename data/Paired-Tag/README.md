# Paired-Tag sequence data

Scope: original 2021 plate-based Paired-Tag, 12 initial barcodes and two 96-well ligation rounds. This is not the later 384-well or droplet chemistry.

Source: [Zhu et al., Supplementary Table 1](https://media.springernature.com/original/springer-static/esm/art%3A10.1038%2Fs41592-021-01060-3/MediaObjects/41592_2021_1060_MOESM3_ESM.xlsx), accessed 17 September 2026. `oligos.csv` transcribes all four worksheets (16 general primers, 36 initial DNA/RT oligos, 96 BC02 oligos and 96 BC03 oligos). Modification notation is preserved.

`barcodes.csv` contains 12 BC01 sequences shared by matched DNA and RNA primers, 96 BC02 sequences, and 96 BC03 sequences, all 5′ to 3′ in Read 2 orientation. BC01 excludes the preceding modality base (A for DNA, T for RNA). BC03 oligos are called R04 in the source table; their 0–3 random phase bases follow the 7-base barcode and are excluded from the barcode field. Phase length is zero for BC01 and BC02 because no phase block belongs to those oligos.

The page's structures are derived from these sequences and the [authors' May 2021 protocol](https://github.com/cxzhu/Paired-Tag/blob/b2f367391aba77b17c833cb5671058ee397a19af/protocol/Protocol_Github.pdf). Read positions were checked against `read2_2r::trim` in [reachtools.h](https://github.com/cxzhu/Paired-Tag/blob/b2f367391aba77b17c833cb5671058ee397a19af/reachtools/reachtools.h). The pinned analysis repository revision is `b2f367391aba77b17c833cb5671058ee397a19af`. The UMI precedes BC03 and is 10 bases long. Use linker-aware extraction because the phase block shifts subsequent segments.

The paper's P7XX sequence contains a 6-base index placeholder; the protocol gives a 7-cycle I1 recipe. The page records both rather than silently equating index length and cycle count. RNA molecules also contain the N5XX i5 index, although the cited sequencing recipe only collects I1. The DNA P5 Universal primer has no i5.

Validation on 17 September 2026: all 244 oligos match the source workbook; the 204 barcode entries have the expected lengths and are unique within each round. All 331,776 combinations of the 36 initial DNA/RT primers, 96 BC02 oligos and 96 BC03 oligos were assembled into synthetic 100-cycle Read 2 sequences and passed the authors’ `read2_2r::trim` for UMI, all three barcodes and modality. HTML nesting, section anchors and local links were also checked. This verifies the documented original chemistry, not sequencing-error tolerance.
