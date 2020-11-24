
<!-- README.md is generated from README.Rmd. Please edit that file -->

# TMEscore

### 1.Introduction

TME infiltration patterns were determined and systematically correlated
with TME cell phenotypes, genomic traits, and patient
clinicopathological features to establish the
[TMEscore](https://cancerimmunolres.aacrjournals.org/content/7/5/737)

TMEscore is a R package to do Tumor microenvironment analysis. Main
advantages: - Provides functionality to calculate Tumor microenvironment
(TME) score (PCA or z-score) - Functions to visulize TME data. -
Identify TME relevant mutaions.

### 2.Installation

The package is not yet on CRAN. You can install from Github:

``` r
# install.packages("devtools")
if (!requireNamespace("TMEscore", quietly = TRUE))
  devtools::install_github("DongqiangZeng0808/TMEscore")
```

### 3.Usage

Main documentation is on the `tmescore` function in the package:

``` r
library('TMEscore')
#> Loading required package: survival
#> Loading required package: survminer
#> Loading required package: ggplot2
#> Loading required package: ggpubr
#> TMEscore v0.1.3  For help: https://github.com/DongqiangZeng0808/TMEscore
#> 
#>  If you use TMEscore in published research, please cite:
#>  Tumor microenvironment characterization in gastric cancer identifies prognostic and imunotherapeutically relevant gene signatures.
#>  Cancer Immunology Research, 2019, 7(5), 737-750
#>  DOI: 10.1158/2326-6066.CIR-18-0436 
#>  PMID: 30842092
```

Example

``` r
tmescore<-tmescore(eset = eset_stad, #expression data
                   pdata = pdata_stad, #phenotype data
                   method = "PCA",
                   classify = T)
head(tmescore)
#>               ID subtype   time status TMEscoreA TMEscoreB  TMEscore
#> 284 TCGA-RD-A8N2    <NA> 118.00      0 -7.306563  13.24346 -20.55003
#> 95  TCGA-BR-A4IV      GS  28.97      1 -6.743132  12.61978 -19.36292
#> 66  TCGA-BR-8371      GS  11.97      1 -7.024702  12.56123 -19.58593
#> 69  TCGA-BR-8380      GS     NA      1 -5.855567  12.97473 -18.83030
#> 101 TCGA-BR-A4J9      GS   0.47      0 -6.643521  11.98279 -18.62631
#> 82  TCGA-BR-8592      GS   6.37      1 -5.143173  12.47427 -17.61744
#>     TMEscore_binary
#> 284             Low
#> 95              Low
#> 66              Low
#> 69              Low
#> 101             Low
#> 82              Low
```

``` r
tmescore<-tmescore[!is.na(tmescore$subtype),]
library(ggplot2)
p<-ggplot(tmescore,aes(x= subtype,y=TMEscore,fill=subtype))+
  geom_boxplot(notch = F,outlier.shape = 1,outlier.size = 0.5)+
  scale_fill_manual(values= c("#0073C2FF", "#CD534CFF", "#58CDD9","#D20A13" ))
p+theme_light()+stat_compare_means(aes(label = paste0("p = ", ..p.format..)))
```

<img src="man/figuresunnamed-chunk-5-1.png" width="100%" />

## References

Manuscript is under review.

E-mail any questions to <dongqiangzeng0808@gmail.com>
