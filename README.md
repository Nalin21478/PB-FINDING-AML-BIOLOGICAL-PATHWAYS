# PB-FINDING-AML-BIOLOGICAL-PATHWAYS
This code performs various analyses and visualizations using the TCGAbiolinks package and several other libraries in R. It retrieves gene expression and DNA methylation data from the TCGA-LAML project and performs similarity network fusion (SNF) to identify clusters and perform differential expression analysis. It also performs gene ontology (GO) enrichment analysis and generates visualizations such as heatmaps, volcano plots, dotplots, barplots, and network graphs.

Required Libraries
TCGAbiolinks
tidyverse
maftools
pheatmap
SummarizedExperiment
sesame
SNFtool
EnhancedVolcano
limma
ggrepel
ggfortify
plotly
edgeR
preprocessCore
proxy
dplyr
stats
clusterProfiler
org.Hs.eg.db
ggplot2
RColorBrewer
enrichplot
igraph
Please make sure to install these libraries before running the code.

Code Description
The code begins by loading all the required libraries.

It retrieves the list of projects using the getGDCprojects() function and then displays the summary of the TCGA-LAML project using the getProjectSummary() function.

It builds a query to retrieve gene expression data from the TCGA-LAML project based on specific criteria such as data category, experimental strategy, workflow type, and access. The query is created using the GDCquery() function.

The getResults() function is used to retrieve the results based on the query.

The data is downloaded using the GDCdownload() function.

The gene expression data is prepared using the GDCprepare() function, and the resulting SummarizedExperiment object is stored in the variable tcga_brca_data. The gene expression matrix is extracted using the assay() function and stored in the variable brca_matrix.

The DNA methylation data is retrieved by building a query similar to the gene expression data query. The GDCquery() function is used to create the query, and the getResults() function retrieves the results.

The DNA methylation data is downloaded using the GDCdownload() function.

Duplicated samples are removed from the DNA methylation data using the duplicated() function.

The DNA methylation data is prepared using the GDCprepare() function, and the resulting SummarizedExperiment object is stored in the variable dna.meth. The DNA methylation matrix is extracted using the assay() function and stored in the variable methyl_data.

A subset of probes showing differences in beta values between samples is selected using the rowVars() and order() functions, and the resulting indices are stored in the variable idx.

The selected probes are visualized using a heatmap created with the pheatmap() function.

Similarity Network Fusion (SNF) is performed on the gene expression and DNA methylation data. The parameters K, alpha, and T are set, and the gene and methylation data matrices are subsetted to include only common samples.

Data normalization and preprocessing are performed on the gene expression and DNA methylation data.

Distance matrices are calculated using the dist() function based on correlation for gene expression data and Euclidean distance for DNA methylation data.

Affinity matrices are computed using the SNFtool package's affinityMatrix() function.

SNF is applied to the affinity matrices using the SNFtool::SNF() function, and the resulting fused data is stored in the snf_result variable.

Spectral clustering is performed on the fused data using the spectralClustering() function, and the resulting cluster assignments are stored in the cluster variable.

Cluster analysis and visualization are performed using various functions from the SNFtool package.

Cluster rows are extracted for each cluster and stored in a list named cluster_rows.

The differential expression analysis is performed using the limma package. A linear model is fitted using the cluster assignments as the design matrix, and empirical Bayes moderation is applied using the eBayes() function. The top differentially expressed genes are extracted using the topTable() function.

Log fold change values are calculated for each cluster and added to the results matrix.

The mean of log fold change values is calculated across all clusters, and a new column named "logfoldchange" is added to the results matrix.

The results matrix is filtered to include only significant genes based on p-value and fold change thresholds.

Volcano plots are generated using the EnhancedVolcano package's EnhancedVolcano() function.

GO enrichment analysis is performed using the cluster-specific gene lists and the enrichGO() function from the clusterProfiler package. The org.Hs.eg.db package is used for gene annotation.

Various plots, such as dotplots, barplots, cnetplots, and goplots, are generated to visualize the GO enrichment results.

Heatmaps are created to visualize the gene expression patterns of significant genes using the heatmap() function.

Network graphs are generated using the igraph package based on the gene-category associations.

Notes
Some commented code lines (denoted by #) are present in the code for reference or possible future use.
The code assumes that the required input data files are available and properly formatted for analysis.
Please note that running the entire code may take a significant amount of time and computational resources, depending on the size and complexity of the data.
