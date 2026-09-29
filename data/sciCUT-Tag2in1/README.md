# sciCUT&Tag / sciCUT&Tag2in1 sequence data

Scope: sciCUT&Tag2in1 from Janssens et al. (2025) [Cell Reports](https://doi.org/10.1016/j.celrep.2025.116802) (PMC13067999). Plate 1 on its own is the sciCUT&Tag design from [Nature Protocols 2024](https://doi.org/10.1038/s41596-023-00905-9).

## Files

- `NIHMS2137280-supplement-Supplementary_Table_1.xlsx` is the unmodified Supplementary Table 1, downloaded from Europe PMC on 29 September 2026.
- `oligos.csv` has all 188 oligos from that table, copied exactly. It adds a `set` column and the 8-bp barcode extracted from each Tn5 adapter or PCR primer, in the same orientation as in the oligo.
- `read_structure.csv` gives 1-based positions for the published NextSeq run (R1 79, I1 43, I2 37, R2 79).

## Notes

- Plate 1 (`P5_s5_1..8` x `P7_s7_1..12`) is the Amini et al. 2014 sci-ATAC-seq Tn5 set, except `P5_s5_4`, which is `TTCTCGTA` here and `GGCTCTGA` in Amini. Plate 2 (`P5_s5_9..16` x `P7_s7_13..24`) is new.
- In the source table `sci_Ad2.60` and `sci_Ad2.61` have the same sequence, and `sci_Ad2.72` is missing (71 i7 primers listed, 72 i5). They are kept as published.
- The authors' demultiplexer is [sciCTextract](https://github.com/mfitzgib/sciCTextract) (checked at `42f99f48ad7fe7ff0485af81ed7ad3e6bc7bef1e`). Its barcode tables give s5 and i5 in oligo orientation, and s7 and i7 as the reverse complement of the oligo.
- The mapping between plate-1 and plate-2 wells, which is needed to pair modalities, is not published.

## Validation (29 September 2026)

- Every Tn5 adapter matches `s5 + 8 nt + GCGATCGAGGACGGC + ME` or `s7 + 8 nt + CACCGTCTCCGCCTC + ME`.
- Every PCR primer matches `P5 + 8 nt + s5` or `P7 + 8 nt + s7`.
- All four custom sequencing primers are 3' substrings of the Amini sci-ATAC-seq primers.
- 9,600 synthetic libraries were built from the oligos (all 384 Tn5 s5 x s7 pairs, including mixed-plate pairs, x 5 i5 x 5 i7). Each gave the documented R1, I1 (43 nt) and I2 (37 nt) contents.
- Parsing these libraries with the sciCTextract slicing logic recovered all four barcodes.
