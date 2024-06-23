# old, outdated abstract

MicroRNAs (miRNAs) are small non-coding RNAs that play crucial roles in various cellular processes, including gene expression regulation, cell proliferation, and apoptosis. They function by binding to complementary sequences on target mRNAs, leading to transcriptional repression or mRNA degradation. Dysregulation of miRNA function has been implicated in various diseases, including cancer, where specific miRNAs can act as oncogenes or tumor suppressors. Somatic mutations in cancer genomes can affect miRNA binding sites, potentially altering miRNA-mediated gene regulation and contributing to tumorigenesis. 

In this study, we aim to investigate the effects of somatic mutations on miRNA binding in the context of mutational signatures. We will train a machine learning model using the XGBoost algorithm, utilizing experimental high-confidence miRNA-mRNA interactions and a set of aggregated features that enable the detection of both canonical and non-canonical bindings. We will then apply our model to somatic mutations from breast cancer patients, obtained from the PCAWG dataset, and evaluate the impact of these mutations on miRNA binding sites. 

By comparing miRNA binding predictions for wild-type and mutated sequences, we will identify mutations that disrupt normal bindings or create de novo bindings. Furthermore, we will analyze the relationship between mutational signatures and the affected miRNA bindings, providing insights into the potential role of specific mutational processes in altering miRNA-mediated gene regulation. 

To gain a broader perspective, we will consider each miRNA within its related miRNA family, enabling us to understand which miRNA families are more affected by the mutations associated with each mutational signature. This approach will help uncover the complex interactions between somatic mutations, mutational signatures, and miRNA-mediated gene regulation in breast cancer. 

The systematic approach described in this study is cancer-type agnostic and can be easily applied to other cancer types. By extending this analysis to the entire PCAWG dataset, we aim to unveil previously unknown regulatory mechanisms and potential therapeutic targets across various cancer types. 

In conclusion, our study aims to elucidate the interconnected nature of somatic mutations, mutational signatures, and miRNA binding in breast cancer. By applying our findings to other cancer types, we seek to contribute to a more comprehensive understanding of the underlying mechanisms driving cancer development and progression. This research has the potential to uncover novel insights into the role of miRNAs in cancer and may ultimately lead to the identification of new therapeutic targets and strategies for cancer treatment.


############# whole project definition

Somatic mutations in cancer genomes are influenced by various exogenous and endogenous mutational processes, each leaving a unique mutational signature. The COSMIC database contains detailed information on the most up-to-date mutational signatures extracted from various cancer types. A recently published study demonstrated the distribution of mutational signatures according to DNA processes and genome organization. 

In the proposed project, we anticipate that investigating the relationships between mutational signatures and microRNAs could provide unique and valuable insights. This approach could uncover the complex interactions between genetic and epigenetic factors involved in cancer development and progression. 

We will train machine learning models using artificial intelligence to predict the effects of somatic mutations on microRNA binding. Using Extreme Gradient Boosting (XGBoost), we will predict whether the binding of microRNAs to the mutated DNA sequence increases (gain of function) or decreases (loss of function). We will first test our developed machine learning model on the mutation and mutational signature data of 560 breast cancer patients, obtain results for all mutations (aggregated mutations) and each mutational signature, optimize the process, and compile the results as a conference paper. Subsequently, we will apply the developed and optimized process to all cancer types in the PCAWG dataset, both within each cancer type and across cancer types, and publish the results as a journal article. 

Considering each microRNA within its related microRNA family will help us understand which microRNA families are more affected by the mutations present in the mutational signature. This project will aid in better understanding the underlying mechanisms of somatic mutations in cancer genomes, specifically focusing on the role of microRNAs.


#### updated abstract

MicroRNAs (miRNAs) are small non-coding RNAs that play crucial roles in various cellular processes, including gene expression regulation, cell proliferation, and apoptosis. Dysregulation of miRNA function has been implicated in various diseases, including cancer, where specific miRNAs can act as oncogenes or tumor suppressors. Somatic mutations in cancer genomes can affect miRNA binding sites, potentially altering miRNA-mediated gene regulation and contributing to tumorigenesis. These somatic mutations are influenced by various exogenous and endogenous mutational processes, each leaving a unique mutational signature, as documented in the COSMIC database.

In this study, we aim to investigate the impact of somatic mutations on miRNA binding in the context of mutational signatures. We will develop a machine learning model using the XGBoost algorithm, trained on experimental high-confidence miRNA-mRNA interactions and a set of aggregated features. This model will predict whether a miRNA can bind to a given mRNA sequence for a sufficient duration to trigger downstream downregulation of its target gene. To assess the effect of mutations, we will generate wild-type and mutant sequence pairs and process them through our pipeline. Both the wild-type and mutant pairs will be evaluated using our trained classifier, which will report if the mutation had no effect on binding, enabled the miRNA to bind or if it disrupted previously occurring miRNA-mediated downregulation. 

Furthermore, we will analyze the relationship between mutational signatures and the affected miRNA bindings, providing insights into the potential role of specific mutational processes in altering miRNA-mediated gene regulation. We will adopt a comprehensive approach by examining individual miRNAs within their respective families, enabling us to identify which miRNA families are more vulnerable to mutations linked to particular mutational signatures. Also, by categorizing each mutation according to its corresponding mutational signature, which serves as a representation of the underlying mutational processes activated within cells, we aim to bridge the gap between the low-level, individual mutations and the high-level mutational processes. This approach will provide a more complete understanding of how these processes contribute to cancer development and progression through their impact on miRNA binding and gene regulation.

This approach is solely sequence based so it is cancer-type and tissue-type agnostic, allowing it to be easily applied to other cancer types, potentially uncovering previously unknown regulatory mechanisms and therapeutic targets across various cancer types.
 
In conclusion, our study aims to elucidate the interconnected nature of somatic mutations, mutational signatures, and miRNA binding in cancer. By applying our findings to multiple cancer types, we seek to contribute to a more comprehensive understanding of the underlying mechanisms driving cancer development and progression. This research has the potential to uncover novel insights into the role of miRNAs in cancer and may ultimately lead to the identification of new therapeutic targets and strategies for cancer treatment.