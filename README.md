# Prediction of Biomarkers and Therapeutic Combinations for Anti-PD-1 Immunotherapy Using The Global Gene Network Association
Owing to a lack of response to the anti-PD1 therapy for most cancer patients, we developed a network approach to infer genes, pathways, and potential therapeutic combinations that are associated  with tumor response to anti-PD1. 

First, the network guilt-by-association method was used to calculate functional relatedness (hereafter termed MHC I association score) of each genes with the MHC I pathway genes (Fig. 1A). Pathways that enrich genes with high association scores would be associated with the anti-PD1 (Fig. 1A).

Third, TCGA data was integrated with the top predicted genes to build up a signature-based response predictor of anti-PD1 for a specific cancer type.

![Fig1](https://user-images.githubusercontent.com/14062661/132103710-29d3e762-5e4a-4c30-85d0-a3a086f9a131.jpeg)
<p align="center">
<b>Fig. 1: The network-based approach</b><br>
</p>


# MIAS
Our prediction successfully identified genes and pathways known to be associated with anti-PD1, and was further validated by 6 CRISPR gene sets associated with tumor resistance to cytotoxic T cells and targets of the 36 compounds that have been tested in clinical trials for combination treatments with anti-PD1. Mapping drug target data to our top prediction also identified inhibitors that could potentially enhance tumor response to anti-PD1, such as inhibitors of CDK, GSK3B, and PTK2.





We hypothesized that aberrations of any gene that are close to MHC class I genes in a gene network are likely to deregulate MHC I pathway and affect tumor response to anti-PD1. Second, pathways that enrich genes with high association scores would be associated with the anti-PD1. Third, TCGA data was integrated with the top predicted genes to build up a signature-based response predictor of anti-PD1 for a specific cancer type. Forth, the drug target data was mapped to the top predicted genes, whose expression are also significantly correlated with the immune score in a cancer type, to identify compounds that could enhance tumor response to anti-PD1.


Integration of our MHC I-association prediction with TCGA transcriptomic data of a given cancer type can select signature genes for calculating the MIAS score to predict patient response to anti-PD1 of that cancer type. 





the MHC I association immunoscore (MIAS) 

# R codes for figures and tables of the manuscript: 
### Prediction of biomarkers and therapeutic combinations for anti-PD-1 immunotherapy using the global gene network association
>1. Download the "MHC_Asso.zip" file to your computer. After unzipping the "MHC_Asso.zip", navigate to the extension folder, "MHC_Asso", and set it as the working directory in R. <br />
>2. Install the required R packages: FusionPathway, fgsea, gplots, ggplot2, gridExtra, reshape2, GeneOverlap, igraph, MASS, RColorBrewer, gridExtra, stringr, e1071, caret, and GSVA(see "Manuscript_Figures_Tables.r") <br />
>3. Run the R script, "Manuscript_Figures_Tables.r", from command line: R CMD BATCH Manuscript_Figures_Tables.r or, run the scripts in "Manuscript_Figures_Tables.r STEP BY STEP in R to generate the figures and tables in the manuscript.  <br />
>4. The scripts has been tested successfully on R 4.0.2 <br />


# Anti-PD1 response predictors for melanoma patient samples 







