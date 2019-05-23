---
title: "activityCounts"
output: rmarkdown::html_vignette
vignette: >
  %\VignetteIndexEntry{activityCounts}
  %\VignetteEngine{knitr::rmarkdown}
  %\VignetteEncoding{UTF-8}
---



<style>
body{
text-align : justify;
line-height: 1.8em;
}
</style>

# Introduction
Health and activity researchers have used accelerometers to study people's movement and activity. There are different brands of accelerometers, and one of the most common ones is Actigraph. Actigraph has a closed source software, ActiLife, which produces a measurement called counts. Although there are many other accelerometers brands, none of them have software to generate the counts measure as Actigraph does.<br> Since there are many studies done using actigraph counts, Brond et al. developed a code in Matlab, which can convert accelerometers data to actigraph counts. Although their work can help researchers to use different accelerometers brands and calculate the counts measure, Matlab is a commercial program. Unlike Matlab, R is open source, and also R is very popular among health and activity researchers. The package activityCounts allow users to convert the accelerometer data to Actigraph counts very quickly.

<br>

# How to use
## Install R
Visit <https://www.r-project.org/> to download and install.

## Install RStudio (recommended)
Although it is not necessary, RStudio makes using R easier. To install the latest version, go to <https://www.rstudio.com/> and download the installation file based on your operating system.

## Install activityCounts

You can install the released version of activityCounts from [CRAN](https://CRAN.R-project.org) with running the following code in the R console:

``` r
install.packages("activityCounts")
```

And the development version from [GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("walkabillylab/activityCounts")
```

## Load activityCounts
To load the package and its sample datasets run the following in R console:



```r
library(activityCounts)
```


## Import your data
To generate the counts, import your data from your source file. Store the data inside a variable so you can pass that the main function of the package, `counts()`. 
For example, you can use the `fread()` function from the `data.table` package to import your data:
Note that the dataset must have three columns which X, Y, and Z readings respectively.

``` r
# install.packages("data.table")
raw_accel_data <- data.table::fread("~/your_raw_accelerometer_data.csv)
```


## Use the counts() function
To generate the counts, provide the function `counts()` with your data and the sampling frequency of the data.

```r
# assume sampling frequency is 100 Hz
sampling_frequency <- 100 
counts_measures <- activityCounts::counts(data = raw_accel_data, hertz = sampling_frequency)
```

Now the variable `counts_measures` contains three columns which indicate the calculated counts for X, Y, and Z axes respectively.

<br>

# Example
activityCounts package includes a sample dataset which by importing the package is available for testing. The name of the dataset is `sampleXYZ` and its sampling frequency is 100Hz. To check out sampleXYZ:


```r
library(activityCounts)
head(sampleXYZ)
#>   Accelerometer X Accelerometer Y Accelerometer Z
#> 1          -0.035           0.816          -0.063
#> 2          -0.047           0.805          -0.023
#> 3          -0.031           0.793          -0.008
#> 4          -0.020           0.809           0.012
#> 5          -0.016           0.844           0.023
#> 6          -0.004           0.879           0.012
```

Now by applying the function `counts()` calculate the counts for sampleXYZ.


```r
sampleXYZ_counts <- counts(data = sampleXYZ, hertz = 100)
head(sampleXYZ_counts)
#>       x  y  z
#> [1,]  4 89 11
#> [2,] 21 48 13
#> [3,] 17 19 14
#> [4,] 22 39 22
#> [5,] 15 21 15
#> [6,] 23 40 34
```