# Predective model at gene level (5_fold_cross_validation)

Author: Safa MADDOURI
Date: 2023-03-01

## Introduction

This code performs a 5-fold cross-validation analysis using a train-test approach. It uses gene expression data to predict the condition (Normal or Tumoral) of patients. The code implements a Lasso regression model for feature selection and prediction. 

## Prerequisites

Before running the code, make sure you have the following:

- R programming language installed
- Required R packages: DESeq2, dplyr, glmnet, org.Hs.eg.db, ComplexHeatmap, circlize

## Input Data

The code expects the following input files:

1. Gene Counts: A CSV file containing the gene expression counts. The first column should contain the gene names, and the remaining columns should correspond to the expression counts for each sample. 

2. Condition File: A CSV file specifying the condition (Normal or Tumoral) for each patient. The file should have two columns: the first column should contain the patient's name, and the second column should contain the condition label.

3. Train Matrices: Five CSV files (train1.csv, train2.csv, train3.csv, train4.csv, train5.csv) containing the train matrices for each fold. Each file should have the same format as the gene counts file, with the first column containing the gene names.

4. Test Matrices: Five CSV files (test1.csv, test2.csv, test3.csv, test4.csv, test5.csv) containing the test matrices for each fold. Each file should have the same format as the gene counts file, with the first column containing the gene names.

## Code Usage

1. Replace the paths and filenames in the code with the appropriate paths and filenames for your input files.

2. Run the code in an R environment. It is recommended to use an integrated development environment (IDE) like RStudio.

3. The code will perform the following steps:

   - Preprocessing: Remove N/A values and filter out genes with count < 100.
   
   - Cross-validation Loop: Perform a 5-fold cross-validation using the train and test matrices. For each fold:
   
     - Train DESeq2 model: Create a DESeq2 dataset and run DESeq2 analysis to identify differentially expressed genes.
     
     - Feature Selection: Apply Lasso regression using the selected genes from DESeq2 analysis.
     
     - Predict Condition: Predict the condition (Normal or Tumoral) for the test samples using the Lasso model.
   
   - Combine Results: Combine the results from each fold into a single table and calculate the ROC curve and AUC.
   
   - Evaluate Performance: Predict labels based on a probability threshold and calculate the confusion matrix, sensitivity, specificity, and balanced accuracy.
   
   - Gene Symbol Conversion: Convert the Ensembl gene names to gene names using the org.Hs.eg.db database.
   
   - Heatmap Visualization: Visualize the scaled gene expression data for the genes selected by deseq2 then by lasso regression for the five folds using a heatmap.
   
## Output

The code produces the following output files:

- ROC.png: A plot of the Receiver Operating Characteristic (ROC) curve.
- lasso_genes_symbolX.csv: Five CSV files (X = 1, 2, 3, 4, 5) containing the selected genes' symbols for each fold.
- all_lassogene_symbol.csv: A CSV file containing all the selected genes' symbols across all folds.
- Heatmap.png: A heatmap visualizing the scaled gene expression data (for the genes selected by deseq2 then by lasso regression for the five folds) for Normal and Tumoral conditions.



