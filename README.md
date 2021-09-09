# Prediction of Biomarkers and Therapeutic Combinations for Anti-PD-1 Immunotherapy Using The Global Gene Network Association
Owing to a lack of response to the anti-PD1 therapy for most cancer patients, we developed a network approach to infer genes, pathways, and potential therapeutic combinations that are associated  with tumor response to anti-PD1. First, the network guilt-by-association method was used to calculate functional relatedness (hereafter termed MHC I association score) of each genes with the MHC I pathway genes (Fig. 1A). Pathways that enrich genes with high association scores would be associated with the anti-PD1 (Fig. 1A).Second, by leveraging gene expression data of samples, we were able to identify genes and pathways that are associated with the anti-PD1 in a specific cancer type or a specific cellular condition (Fig. 1B). Third, TCGA transcriptomic data can be integrated with the top MHC I-associated genes to select the gene signature and calculate the MHC I association immunoscore (MIAS) to predict patient response to anti-PD1 for a given cancer type. Forth, mining TCGA genetic data using the top MHC I-associated genes can also explore genetic and epigenetic aberrations associated with anti-PD-1 in a given cancer type. Fifth, mapping the drug target data to the top MHC I-associated genes can identify compounds that could enhance tumor response to anti-PD1.

![Fig1](https://user-images.githubusercontent.com/14062661/132103710-29d3e762-5e4a-4c30-85d0-a3a086f9a131.jpeg)
<p align="center">
<b>Fig. 1: The network-based approach</b><br>
</p>

Our prediction successfully identified genes and pathways known to be associated with anti-PD1, and was further validated by 6 CRISPR gene sets associated with tumor resistance to cytotoxic T cells and targets of the 36 compounds that have been tested in clinical trials for combination treatments with anti-PD1. Mapping drug target data to our top MHC I-associated genes also identified inhibitors that could potentially enhance tumor response to anti-PD1, such as inhibitors of CDK, GSK3B, and PTK2. The MIAS score showed a good correlation with patient response to anti-PD1 for 411 melanoma samples complied from 6 cohorts. 


# R codes for figures and tables of the manuscript: 
>1. Download the "MHC_Asso.zip" file to your computer. After unzipping the "MHC_Asso.zip", navigate to the extension folder, "MHC_Asso", and set it as the working directory in R. <br />
>2. Install the required R packages: FusionPathway, fgsea, gplots, ggplot2, gridExtra, reshape2, GeneOverlap, igraph, MASS, RColorBrewer, gridExtra, stringr, e1071, caret, and GSVA(see "Manuscript_Figures_Tables.r") <br />
>3. Run the R script, "Manuscript_Figures_Tables.r", from command line: R CMD BATCH Manuscript_Figures_Tables.r or, run the scripts in "Manuscript_Figures_Tables.r STEP BY STEP in R to generate the figures and tables in the manuscript.  <br />
>4. The scripts has been tested successfully on R 4.0.2 <br />

# Response prediciton using trained MIAS-IMPRES predictors
Our analysis also showed that the integration of the MIAS and IMPRES scores also have a better prediction performance than the two individual method (Fig. 6D in the manuscript). 
We used the MIAS and <a href="https://www.nature.com/articles/s41591-019-0671-4">IMPRES </a> scores of the collected 411 melanoma samples as the data fetures to train two predictors of anti-PD1 response using support vector machine (SVM) respectively for pre- and on-treated SKCM patient samples. These two predictors can help people to predict responses of SKCM patient samples using their transcriptomic data.

Install and load the require R packages
> library(e1071)  #svm <br />
> library(GSVA) <br />

Load the data file containing the 4 pre-trained predictors: MIAS.Classifier_Pre,MIAS.Classifier_On, MIAS.IMPRES.Classifier_Pre, and MIAS.IMPRES.Classifier_On.
>load("./data/Response.Predictors_PD1_SKCM.RData") <br />

Load the gene expressio data of the melanoma patient samples for response prediction. Here, an example dataset (<a href="https://www.cell.com/cell/comments/S0092-8674(17)31122-4">Riaz, et al 2017</a>) was loaded.
> load("./data/Example.Data_Riaz.2017.RData")	<br />

Seperate data of pre- and on-treatment samples
> DataM_EX.Pre<-DataM_EX[,which(PreOn=="Pre")]  <br />
> Response.Pre<-Response[which(PreOn=="Pre")]	<br />
> DataM_EX.On<-DataM_EX[,which(PreOn=="On")]	<br />
> Response.On<-Response[which(PreOn=="On")]	<br />

Load the selected SKCM signature genes for calculating MIAS scores (The signature genes were selected by integrative analysis of our MHC I-association prediction and TCGA SKCM transcriptomic data).
> filein="./data/Table.S6_Immune_positive signature.xls"  <br />
> DataM1 <- read.table(filein,sep="\t",header=T, quote="") <br />
> Signatures_M<-NULL  <br />
> Signatures_M[[1]]=as.character(DataM1[[1]])  <br />

Calculate the MIAS and IMPRES Scores of the pre- and on-treatment samples
> MIAS_Score.Pre<-MIAS.Score.GSVA(DataM_EX.Pre,Signatures_M)  <br />
> IMPRES_Score.Pre<-IMPRES.Score(DataM_EX.Pre)  <br />
> MIAS_Score.On<-MIAS.Score.GSVA(DataM_EX.On,Signatures_M)  <br />
> IMPRES_Score.On<-IMPRES.Score(DataM_EX.On)  <br />

Do the response prediction of the on-treatment samples using the on-treatment predictor that were trained using both of MIAS and IMPRES scores (MIAS.IMPRES.Classifier_On)
> data_set.On<-data.frame(MIAS=MIAS_Score.On,IMPRES=IMPRES_Score.On,Response=Response.On) <br />
> prediction.On = predict(MIAS.IMPRES.Classifier_On, newdata = data_set.On[-3], probability =T)  <br />
> response.probabilities.On<-attr(prediction.On,"probabilities")[,2]  <br />
> cf = table(data_set.On[, 3], prediction.On)  <br />
> accuracy.On = (cf[1,1] + cf[2,2]) / (cf[1,1] + cf[2,2] + cf[1,2] + cf[2,1])  <br />
> accuracy.On  <br />

We can also do the response prediction of the pre-treatment samples using the pre-treatment predictor (the script was not listed here)







