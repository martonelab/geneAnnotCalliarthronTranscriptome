KEGG KO mapping for Calliarthron Genome
================
Jan Xue
April 29 2019

KEGG Based Identification of Metabolic Pathways in Calliarthron's Transcriptome
-------------------------------------------------------------------------------

### Overview

This script is meant to allow users to find pathways of interest within the Calliarthron transcriptome presented. This is based on annotations from the [Kyoto Encyclopedia of Genes and Genomes](https://www.genome.jp/kegg/) (KEGG).

To identify patways of interest to you, first visit the KEGG website and look up the identification code by clicking [here](https://www.genome.jp/kegg/pathway.html).

There you will find a identification code that corresponds to a particular pathway. For example:

**01100 Metabolic pathways**

Here "01100" is the identifier code that you will need in order to continue with this script. "Metabolic pathways" reffers to the particular type of patway presented. On the website you can click on the pathway name in order to learn more about it.

Below is a short tutorial of how to utilize this script.

### Load Packages

These packages were used in order to run this script.

``` r
#install pthview if it is not present, highlight the bottom two lines and press cmd+shift+C to uncomment
source("https://bioconductor.org/biocLite.R")
biocLite("pathview")
```

    ## 
    ## The downloaded binary packages are in
    ##  /var/folders/xw/1hj3qd6122v2pw__lwlcsmy00000gn/T//RtmpMpignu/downloaded_packages

``` r
#load pathview
library(pathview)
```

``` r
#install.packages("readxl")
#load package
library("readxl")
library(ggplot2)
library(plyr)
library(tidyverse)
library(ggpubr)
library(dplyr)
```

### Organizing the Data

This was how I originally reorganized the data. You can skip ahead to *Pathway Extraction* if you are not interested in this overview.

#### Reading in the Data

I have a file from CX that has the KO identifiers and the KO identifiers and associated contig from the calliarthron contig. For these purposes I will be using a combined dataset.

In order to make this more meaningful for future extraction of data, I will be combining the contig names from the transcriptome assembly and the KEGG or KO identifiers that have the protein description and EC numbers.

``` r
# join the two datafiles to make a master metadata file
md <- left_join(combinedKO, identKO, by = "KO_Identifier")
```

#### Extract Pathway Function

In order to simplify obtaining the patway for users, a predefined function has been written. See below to find the specification of the function.

**Note** : You need to be connected to the internet in order for this to work.

``` r
# caPathGet
# 
# Get a specific KEGG pathway and presence of sequences from the calliarthron transcriptome. Produces ong file with KEGG annotation of sequence presence. Then produces a dataframe containing all of the sequences in the pathway and the one mapped and their metadata. REmoves unecessary columns
# @param pathID     - A 5 digit code that identifies which pathway you want to use
# @param fileSuffix     - what you want to name your file suffix, likely you want to use the pathway name
# @param color     - you can specify the color you want your genes present to be
# 
# @return the png image of the KEGG pathway

caPathGet = function(pathID, fileSuffix, color)
{
    pv <- pathview(gene.data = md$KO_Identifier, 
                   pathway.id = pathID, 
                   species = "ko", 
                   out.suffix = fileSuffix, 
                   kegg.native = T,
                   high = list(gene = color, cpd =
                    "yellow"))
    
    matchNames <- pv$plot.data.gene
    colnames(matchNames)[1] <- "KO_Identifier"
    
    idPath <- left_join(matchNames, md, by = "KO_Identifier") %>%   
      distinct(KO_Identifier, .keep_all = TRUE)
    idPath$labels = NULL
    idPath$type = NULL
    idPath$x = NULL
    idPath$y = NULL
    idPath$width = NULL
    idPath$height = NULL
    idPath$mol.data = NULL
    idPath$mol.col = NULL
    
    return(idPath)
    
}
```

### Pathway Extraction

This is an example to demonstrate how to obtain a pathway from the Calliarthron transcriptome based on annoations from KEGG.

The format is as shown, bolded items indicate user defined settings.

**Name\_You\_Define\_A** &lt;- caPathGet("**KO\_Identifier**", "**Name of Pathway**", "**Color**")

Then another file is written to extract the contigs in the transcriptome that corresponds to the parts of the pathway that are present. This should be present in the results folder.

write.table(**Name\_You\_Define\_A**, "Results/Tables/**Name\_You\_Define\_A**.txt", sep="")

For an example see below

``` r
# Get the pathway for calcium signalling
CalciumSignallingPathway04020 <- caPathGet("04020", "CalciumSignallingPathway", "#FA8072")

# write the results to a table
write.table(CalciumSignallingPathway04020, "Results/Tables/CalciumSignallingPathway.04020.txt", sep="\t")
```
