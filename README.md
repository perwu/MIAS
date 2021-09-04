# MIAS
Owing to a lack of response to the anti-PD1 therapy for most cancer patients, we developed a network approach to infer genes, pathways, and potential therapeutic combinations that are associated  with tumor response to anti-PD1.  Our prediction successfully identified genes and pathways known to be associated with anti-PD1, and was further validated by 6 CRISPR gene sets associated with tumor resistance to cytotoxic T cells and targets of the 36 compounds that have been tested in clinical trials for combination treatments with anti-PD1. Mapping drug target data to our top prediction also identified inhibitors that could potentially enhance tumor response to anti-PD1, such as inhibitors of CDK, GSK3B, and PTK2.






the MHC I association immunoscore (MIAS) 

# R codes for figures and tables of the manuscript: 
### Prediction of biomarkers and therapeutic combinations for anti-PD-1 immunotherapy using the global gene network association
>1. Download the "MHC_Asso.zip" file to your computer. After unzipping the "MHC_Asso.zip", navigate to the extension folder, "MHC_Asso", and set it as the working directory in R. <br />
>2. Install the required R packages: FusionPathway, fgsea, gplots, ggplot2, gridExtra, reshape2, GeneOverlap, igraph, MASS, RColorBrewer, gridExtra, stringr, e1071, caret, and GSVA(see "Manuscript_Figures_Tables.r") <br />
>3. Run the R script, "Manuscript_Figures_Tables.r", from command line: R CMD BATCH Manuscript_Figures_Tables.r or, run the scripts in "Manuscript_Figures_Tables.r STEP BY STEP in R to generate the figures and tables in the manuscript.  <br />
>4. The scripts has been tested successfully on R 4.0.2 <br />


# R codes of anti-PD1 response prediction for melanoma patient samples 







