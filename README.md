# Genome Assembly and Alignment - *Salmonella enterica*

## Introduction

Through the use of Salmonella enterica raw reads from an Oxford Nanopore sequencer (expected accuracy Q20+, N50:5-15kb), this work aims to assemble a consensus genome of high quality through established long-read assembly methods. The generated genome would then be compared to a reference genome from NCBI for Salmonella enterica, which would then be visualized for further analysis. 

Genome assembly can pose challenges such as ensuring accuracy with genome construction, especially when further analysis requires a high-quality genome. Long-read sequences tend to have higher error rates compared to short-read sequences, although recent improvements have led to more accurate results with long-read data alone through Oxford Nanopore sequencing (Zhao et al., 2023). Computational demands may also slow the progress of genome assembly and further analysis, so a pipeline with optimally balanced tools should be considered.

A quality control tool was chosen to identify the condition of the raw Nanopore reads before further assembly and analysis were conducted. NanoPack was chosen due to its specific purpose of processing Nanopore reads, along with the inclusion of Nanoplot for data analysis (De Coster, 2018). A recent study looking at the use of Oxford nanopore long-read sequencing for genome assembly found that for a 5 Mb bacterial genome, accuracies of over 99.99% were achieved through the usage of Flye and Medaka for assembly and polishing (Zhao et al., 2023). Another study looking at the Salmonella enterica genome across 341 strains found that the average lengths of genomes ranged from 4.50 to 5.15 Mb, within the range of 5 Mb for high accuracy scores through Flye and Medaka (Lyu et al., 2021). Therefore, the combination of Flye and Medaka was considered for this project. Other assembly tools, such as Canu and NECAT, also deliver accurate results in comparison studies, however potentially lead to slower processing times (Kumar et al., 2025). Minimap2 was chosen as the aligner for this project as it is considered to be high-performance for Nanopore reads, although studies have identified potential improvements for speed (Sadasivan, 2023). Clair3, a deep learning tool designed for long-read sequencing data, was used to perform variant calling and has performed highly in previous studies compared to previous techniques (Hall et al., 2024). Overall, this approach aims to provide a practical pipeline for comparing assembled and referenced genomes. 

## Proposed Methods

### Read Acquisition 

The data collected from NCBI contained Nanopore long-reads in the FASTQ format. Further analysis was conducted on the Compute Canada Fir cluster. Assembly and analysis tools were installed through the miniconda (v. 25.11.1) package manager through the Ubuntu terminal. A complete Salmonella enterica reference genome was retrieved from the NCBI database and used for alignment. 

### Read Processing

Raw Nanopore reads were assessed for quality using NanoPlot (v. 1.46.2) with parameter `--fastq` (De Coster et al., 2018). Nanopack (v. 1.1.1) was used for further read edits as necessary (De Coster et al., 2018). 

### Genome Assembly and Polishing 

Genome assembly was performed through the use of Flye and default parameters (v. 2.9.6) (Kolmogorov et al., 2019). 

Polishing was done through the use of Medaka (v. 2.1.1) (Oxford Nanopore Technologies, 2025). 

### Genome Alignment

In order to align the assembled genome to the reference, minimap2 was used with the `-ax asm5` flag (v. 2.30), the alignments were then converted to BAM using samtools (v. 1.23) (Li, 2018);(Li et al., 2009). 

### Variant Calling

Variant calling between raw reads and the reference assembly was performed through the usage of clair3 (v. 1.20) installed through miniconda for further analysis of the reads. 

### Result Visualisation

Aligned reads were visualized in Integrative Genomics Viewer (IGV) (v. 2.19.7) (Robinson et al., 2011) through the transfer of files locally. 

## References

Anaconda Inc. (2025). Miniconda (Version 25.11.1). Anaconda.

De Coster, W., D’Hert, S., Schultz, D. T., Cruts, M., & Van Broeckhoven, C. (2018). NanoPack: Visualizing and processing long-read sequencing data. Bioinformatics, 34(15), 2666–2669. https://doi.org/10.1093/bioinformatics/bty149

Hall MB, Wick RR, Judd LM, Nguyen AN, Steinig EJ, Xie O, Davies M, Seemann T, Stinear TP, Coin L. Benchmarking reveals superiority of deep learning variant callers on bacterial nanopore sequence data. Elife. 2024 Oct 10;13:RP98300. doi: 10.7554/eLife.98300 PMID: 39388235; PMCID: PMC11466455

Kolmogorov, M., Yuan, J., Lin, Y., & Pevzner, P. A. (2019). Assembly of long, error-prone reads using repeat graphs. Nature Biotechnology, 37(5), 540–546. https://doi.org/10.1038/s41587-019-0072-8

Kumar, M. S., Krishna, M. B., Soman, K. P., Stanley, J., Pourmand, N., Suravajhala, P., & Babu, T. G. S. (2025). Benchmarking long-read assembly tools and preprocessing strategies for bacterial genomes: A case study on E. coli DH5α. Biotechnology Reports, 48, Article e00931. https://doi.org/10.1016/j.btre.2025.e00931

Li, H., Handsaker, B., Wysoker, A., Fennell, T., Ruan, J., Homer, N., Marth, G., Abecasis, G., Durbin, R., & 1000 Genome Project Data Processing Subgroup. (2009). The Sequence Alignment/Map format and SAMtools. Bioinformatics, 25(16), 2078-2079. https://doi.org/10.1093/bioinformatics/btp352

Li, H. (2018). Minimap2: Pairwise alignment for nucleotide sequences. Bioinformatics, 34(18), 3094–3100. https://doi.org/10.1093/bioinformatics/bty19

Lyu, N., Feng, Y., Pan, Y., Huang, H., Liu, Y., Xue, C., Zhu, B., & Hu, Y. (2021). Genomic characterization of Salmonella enterica isolates from retail meat in Beijing, China. Frontiers in Microbiology, 12, 636332. https://doi.org/10.3389/fmicb.2021.636332

Oxford Nanopore Technologies. (2025). Medaka: Sequence correction provided by ONT Research (Version 2.2.0). GitHub.

Robinson, J. T., Thorvaldsdóttir, H., Winckler, W., Guttman, M., Lander, E. S., Getz, G., & Mesirov, J. P. (2011). Integrative genomics viewer. Nature biotechnology, 29(1), 24–26. https://doi.org/10.1038/nbt.1754

Sadasivan, H., Maric, M., Dawson, E., Iyer, V., Israeli, J., & Narayanasamy, S. (2023). Accelerating Minimap2 for Accurate Long Read Alignment on GPUs. Journal of biotechnology and biomedicine, 6(1), 13–23. https://doi.org/10.26502/jbb.2642-91280067

Zhao, W., Zeng, W., Pang, B., Luo, M., Peng, Y., Xu, J., Kan, B., Li, Z., & Lu, X. (2023). Oxford nanopore long-read sequencing enables the generation of complete bacterial and plasmid genomes without short-read sequencing. Frontiers in microbiology, 14, 1179966. https://doi.org/10.3389/fmicb.2023.1179966


