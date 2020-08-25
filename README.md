
Transcriptome of the coralline alga Calliarthron tuberculosum (Corallinales, Rhodophyta) reveals parallel evolution of lignin biosynthesis
=======
[![paper](https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Continuous_form_paper_%2814p875_x_11%29.jpg/330px-Continuous_form_paper_%2814p875_x_11%29.jpg=Download)](https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Continuous_form_paper_%2814p875_x_11%29.jpg/330px-Continuous_form_paper_%2814p875_x_11%29.jpg)



Purpose of this page
------------
This page should provide you with the tools to:
- Extract genes from *Calliarthron* (using annotations from KEGG analysis)
- Extract whole metabolic pathways from *Calliarthron* (using the pathview package (1))
- Identify *Calliarthron* sequences with genome support

Introduction
------------
*Calliarthron* is a coralline red algae whoes transcriptome and genome have been recently sequenced. The trasncriptomic data has been annotated with [KEGG](https://www.genome.jp/kegg/pathway.html). Here we provide a method for extracting genes directly.

The raw data can be found 
- **Transcriptome data**: accession [PRJEB39919](link to ENA location)
- **Genome data**: accession [PRJEB39919](link to ENA location)


![CalliarthronImage](http://www3.botany.ubc.ca/martone/gallery-images/22.jpg)


Files
------------
The following three files are downloadable and are easily searchable for quick identification of genes you're interested in.
- **SupFile1_Calliarthron_combined_transcriptome_w_genomeHit.txt** - This file contains all the sequence IDs form the transcriptome that also have genomic support
- **SupFile2_Calliarthron_KEGG_Identifiers.txt** - This file contains all the sequence IDs and their gene annotation from the transcriptome. This is based on KEGG annotation.
- **SupFile3_Calliarthron_Trinity_combined.txt.zip** - This file contains the sequence IDs and their associated sequence.

To extract *Calliarthron* sequences that are annotated as present in a particular metabolic pathway download the file
- CalliarthronKEGGExtraction
In order to do the next steps, you will need to have [RStudio](https://rstudio.com/). Once you've downloaded the file, you'll open up the file on your computer:
- KEGGKOMappingCalliarthron.Rmd
There you'll find detailed instructions of how to extract a pathway and get something like this.

![flowChart](https://github.com/martonelab/geneAnnotCalliarthronTranscriptome/blob/master/images/GeneIdentFlowChart.pdf)
Fig 1. By the end of this tutorial you should be able to extract the *Calliarthron* sequences in a pathway of interest and a list of the sequences present.

Citations
-----------
Luo, Weijun, Brouwer, Cory (2013). “Pathview: an R/Bioconductor package for pathway-based data integration and visualization.” Bioinformatics, 29(14), 1830-1831. doi: 10.1093/bioinformatics/btt285.
