# Droplet Paired-Tag (10x Next GEM Multiome)

Scope: Xie et al. (2023), Chromium X / Chip J, Next GEM Multiome ARC-v1. This is a separate chemistry from the original split-pool Paired-Tag and does not describe later GEM-X kits.

## Sources

- [Paper](https://doi.org/10.1038/s41594-023-01060-1).
- [Four custom oligos](https://github.com/Xieeeee/Droplet-Paired-Tag/blob/d42c0fe0295bd5cb846aa19d1fd49bd0a80ea3a3/03.protocol/Supplementary_Table1_Oligo_Sequence.xls) and [protocol](https://github.com/Xieeeee/Droplet-Paired-Tag/blob/d42c0fe0295bd5cb846aa19d1fd49bd0a80ea3a3/03.protocol/Droplet_Paired-Tag_ProtocolExchange_230719.pdf) from the authors' repository at `d42c0fe0295bd5cb846aa19d1fd49bd0a80ea3a3`, accessed 17 September 2026.
- [10x CG000338, Rev F](../10X-Genomics/CG000338_ChromiumNextGEM_Multiome_ATAC_GEX_User_Guide_RevF.pdf), already present in this repository, supplies the commercial library architecture. It does not establish the complete sequences of proprietary primer mixes; these are schematic in the page.
- [Authors' complete barcode map](https://github.com/Xieeeee/Droplet-Paired-Tag/blob/d42c0fe0295bd5cb846aa19d1fd49bd0a80ea3a3/01.pre-process/supp/arc_bc-translation.txt); [10x translation/tag documentation](https://www.10xgenomics.com/support/software/cell-ranger-arc/latest/analysis/atac-barcoded-bam).

## Files and orientation

`oligos.csv` preserves all four oligos and modification annotations exactly. AdapterA is 5′ phosphorylated; AdapterB is not annotated as phosphorylated. pMENTs is 3′ blocked; pMENTs-Bridge is not annotated with ddC. The bridge is the reverse complement of `CGCGTCTG` followed by the complete AdapterA nucleotide sequence. Its 3′ end complements the bead spacer.

`read_structure.csv` records 1-based inclusive positions for the published NextSeq 2000 settings: DNA 100/8/24/100 and RNA 28/10/10/72 (R1/I1/I2/R2). The DNA I2 subregions describe raw reverse-complement-workflow cycles: 8-base spacer then 16-base cell barcode. Converted FASTQs can differ in orientation and spacer retention. These coordinates must not be reapplied blindly to already trimmed index reads or custom dark-cycle output. RNA carries a 12-base UMI; DNA does not.

`barcode_translation_examples.csv` contains only the first four entries from the authors' map, with its original barcode orientation preserved. It is an example, not a complete whitelist. The existing `../10X-Genomics/atac_737K-arc-v1.txt.gz` and `gex_737K-arc-v1.txt.gz` provide the complete paired references; preserve row order. Index reverse complementation and DNA-to-RNA barcode translation are separate operations. ARC's ATAC CB tag is already translated to GEX identity, whereas CR is raw.

Validation on 17 September 2026: all four custom oligos match the authors’ XLS exactly. The bridge is the exact reverse complement of spacer + AdapterA, and both mosaic ends pair with pMENTs. All 736,320 barcode pairs match the existing two whitelist files in order, are 16-base A/C/G/T sequences and are unique on each side. Synthetic 24-cycle DNA I2 and 28-cycle RNA R1 reads built for every pair satisfy the documented read coordinates. All 10 read-coordinate records cover their reads without gaps or overlaps. HTML nesting, navigation anchors and local links were checked. These are sequence-architecture checks, not a test of a complete sequencing-data pipeline.
