
<!-- README.md is generated from README.Rmd. Please edit that file -->

# PRECISE

## Personalized Integrated Network Modeling

<!-- badges: start -->

<!-- badges: end -->

## Web applet

PRECISE can be used as a web application found at
[BayesRx](https://mjha.shinyapps.io/PRECISE/).

Find out more about the BayesRx group here: [BayesRx
Homepage](https://bayesrx.github.io/).

## Installation

This package depends on packages that not are in CRAN. Install these
prerequisite packages prior to installing PRECISE:

``` r
install.packages("BiocManager")
BiocManager::install(c("graph", "RBGL", "BMS"))
```

You can now install PRECISE from
[Github](https://github.com/umich-biostatistics/PRECISE)
with:

``` r
install.packages("devtools")  # you need devtools to install R packages from Github
devtools::install_github("umich-biostatistics/PRECISE")
```

## Example

``` r
library(PRECISE)  # load PRECISE
```

``` r
data(rppadat)
RPPAdat = rppadat[[1]] # RPPA data for Apoptosis pathway
p = ncol(RPPAdat)
B = 100
alpha = 0.1
alpha.array = seq(0.0001, 0.1, length = 100) 
#pcfit = fitPC(dat = RPPAdat, alpha = alpha, stable = TRUE, 
#              alpha.array = alpha.array, B = B, labels = as.character(1:p), verbose = T) 
data(pcfit)
pcfit = pcfit.list[[1]] # the fitPC result for Apoptosis pathway 

#  make the results from the ﬁtPC function into weighted adjacency matrix as follows
adj.pc = as(pcfit$fit@graph, "matrix") 
addr = matrix(as.numeric(pcfit$rownames), ncol = 2)
addr.rev = cbind(addr[,2], addr[,1]) 
adj.pc[addr] = adj.pc[addr] * pcfit$pcmaxSel[,1]
adj.pc[addr.rev] = adj.pc[addr.rev] * pcfit$pcmaxSel[,2] 
adj.pc
#>   1    2    3 4    5 6    7    8 9
#> 1 0 0.00 0.76 0 0.00 0 0.00 0.89 0
#> 2 0 0.00 0.00 0 0.00 0 0.00 1.00 0
#> 3 0 0.00 0.00 0 0.42 0 0.64 0.48 0
#> 4 0 0.00 0.00 0 0.33 0 0.73 0.91 0
#> 5 0 0.00 0.00 0 0.00 0 0.00 0.00 0
#> 6 0 0.44 0.40 0 0.00 0 0.00 0.00 0
#> 7 0 0.00 0.00 0 0.00 0 0.00 0.00 0
#> 8 0 0.00 0.00 0 0.00 0 0.00 0.00 0
#> 9 0 0.00 0.00 0 0.00 0 0.00 0.96 0
```

## Getting help

For further illustration of PRECISE, see the vignette included with the
package. To see the available vignettes, use
`browseVignettes("PRECISE")`. You can read a specific vignette with
`vignette(PRECISE)`.
