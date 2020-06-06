
<!-- README.md is generated from README.Rmd. Please edit that file -->

# craninfo

<!-- badges: start -->

[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)
<!-- badges: end -->

The goal of `checkinfo` is to surface `CRAN` checks information into a
[sessioninfo](https://github.com/r-lib/sessioninfo) output specific to
the user’s platform.

## Installation

``` r
# install.packages("remotes")
remotes::install_github("yonicd/craninfo")
```

## Example

This is a basic example which shows you how to solve a common problem:

``` r
library(craninfo)
```

On CRAN each package is continually checked to see if there are any
problems with it on a variety of platforms and this information is
always available for package users to view.

[cchecks](https://github.com/ropenscilabs/cchecks) is an R package that
uses an API to retrieve information from these tests in an efficient
manner.

Here is the output from `dplyr`

``` r
(cchecks::cch_pkgs('dplyr'))$data$checks
#>                               flavor version tinstall tcheck ttotal status
#> 1  r-devel-linux-x86_64-debian-clang   1.0.0    17.87 168.83 186.70     OK
#> 2    r-devel-linux-x86_64-debian-gcc   1.0.0    14.50 129.04 143.54     OK
#> 3  r-devel-linux-x86_64-fedora-clang   1.0.0     0.00   0.00 229.62   NOTE
#> 4    r-devel-linux-x86_64-fedora-gcc   1.0.0     0.00   0.00 219.33   NOTE
#> 5        r-devel-windows-ix86+x86_64   1.0.0     3.00   8.00  11.00  ERROR
#> 6             r-patched-linux-x86_64   1.0.0    17.81 165.70 183.51     OK
#> 7              r-patched-solaris-x86   1.0.0     0.00   0.00 258.80   NOTE
#> 8             r-release-linux-x86_64   1.0.0    17.04 164.00 181.04     OK
#> 9               r-release-osx-x86_64   1.0.0     0.00   0.00   0.00   NOTE
#> 10     r-release-windows-ix86+x86_64   1.0.0    58.00 363.00 421.00     OK
#> 11               r-oldrel-osx-x86_64   1.0.0     0.00   0.00   0.00   NOTE
#> 12      r-oldrel-windows-ix86+x86_64   1.0.0    50.00 322.00 372.00     OK
#>                                                                                       check_url
#> 1  https://www.R-project.org/nosvn/R.check/r-devel-linux-x86_64-debian-clang/dplyr-00check.html
#> 2    https://www.R-project.org/nosvn/R.check/r-devel-linux-x86_64-debian-gcc/dplyr-00check.html
#> 3  https://www.R-project.org/nosvn/R.check/r-devel-linux-x86_64-fedora-clang/dplyr-00check.html
#> 4    https://www.R-project.org/nosvn/R.check/r-devel-linux-x86_64-fedora-gcc/dplyr-00check.html
#> 5        https://www.R-project.org/nosvn/R.check/r-devel-windows-ix86+x86_64/dplyr-00check.html
#> 6             https://www.R-project.org/nosvn/R.check/r-patched-linux-x86_64/dplyr-00check.html
#> 7              https://www.R-project.org/nosvn/R.check/r-patched-solaris-x86/dplyr-00check.html
#> 8             https://www.R-project.org/nosvn/R.check/r-release-linux-x86_64/dplyr-00check.html
#> 9               https://www.R-project.org/nosvn/R.check/r-release-osx-x86_64/dplyr-00check.html
#> 10     https://www.R-project.org/nosvn/R.check/r-release-windows-ix86+x86_64/dplyr-00check.html
#> 11               https://www.R-project.org/nosvn/R.check/r-oldrel-osx-x86_64/dplyr-00check.html
#> 12      https://www.R-project.org/nosvn/R.check/r-oldrel-windows-ix86+x86_64/dplyr-00check.html
```

What if you wanted to use this same information to create an output
similar to sessioninfo, but append to it the information from the
current CRAN checks for each loaded namespace (package) tailored to your
platform.

This is what `craninfo` does for you\!

With this information you can

  - See if there are any problems with the packages that you are using
    in an R/Rmd script
  - Attach it to a {reprex} to help the maintainer help you even more
    efficiently.
  - See if you have the most current version of a package installed, and
    if not you can decide if you should install it given it’s current
    CRAN status.
  - Compare multiple CRAN check flavors with ease.

## Console Output

### Current CRAN release

``` r
craninfo()
#> ── Check Info (Sys.time: 2020-06-06 15:31:57) ───────────────────────────
#> ── Flavor: release-osx-x86_64 ───────────────────────────────────────────
#>        package                                    source       date     loaded cran_version release  
#> 1           ps                            CRAN (R 3.6.2) 2020-05-08      1.3.3        1.3.3   ERROR  
#> 2         curl                            CRAN (R 3.6.0) 2019-12-02        4.3          4.3    WARN  
#> 3    ipaddress                            CRAN (R 3.6.2) 2020-05-12      0.3.0        0.3.0    NOTE  
#> 4      iptools                            CRAN (R 3.6.0) 2018-12-09      0.6.1        0.6.1    NOTE  
#> 5         Rcpp                            CRAN (R 3.6.3) 2020-04-09    1.0.4.6      1.0.4.6    NOTE  
#> 6        readr                            CRAN (R 3.6.0) 2018-12-21      1.3.1        1.3.1    NOTE  
#> 7    rmarkdown        Github (rstudio/rmarkdown@18ba267) 2020-01-30      2.1.1          2.2    NOTE *
#> 8      stringi                            CRAN (R 3.6.1) 2020-02-17      1.4.6        1.4.6    NOTE  
#> 9      stringr                            CRAN (R 3.6.0) 2019-02-10      1.4.0        1.4.0    NOTE  
#> 10    urltools                            CRAN (R 3.6.0) 2019-04-14      1.7.3        1.7.3    NOTE  
#> 11 AsioHeaders                            CRAN (R 3.6.0) 2020-03-11   1.12.2-1     1.12.2-1      OK  
#> 12  assertthat                            CRAN (R 3.6.0) 2019-03-21      0.2.1        0.2.1      OK  
#> 13   backports                            CRAN (R 3.6.2) 2020-05-13      1.1.7        1.1.7      OK  
#> 14         cli                            CRAN (R 3.6.0) 2020-02-28      2.0.2        2.0.2      OK  
#> 15      crayon                            CRAN (R 3.6.0) 2017-09-16      1.3.4        1.3.4      OK  
#> 16        crul                            CRAN (R 3.6.0) 2019-11-06      0.9.0        0.9.0      OK  
#> 17        desc               Github (r-lib/desc@da19501) 2020-04-03 1.2.0.9000        1.2.0      OK *
#> 18      digest                            CRAN (R 3.6.0) 2020-02-23     0.6.25       0.6.25      OK  
#> 19    ellipsis                            CRAN (R 3.6.2) 2020-05-15      0.3.1        0.3.1      OK  
#> 20    evaluate                            CRAN (R 3.6.0) 2019-05-28       0.14         0.14      OK  
#> 21       fansi                            CRAN (R 3.6.0) 2020-01-08      0.4.1        0.4.1      OK  
#> 22        glue                            CRAN (R 3.6.2) 2020-05-13      1.4.1        1.4.1      OK  
#> 23         hms                            CRAN (R 3.6.0) 2020-01-08      0.5.3        0.5.3      OK  
#> 24    httpcode                            CRAN (R 3.6.2) 2020-04-10      0.3.0        0.3.0      OK  
#> 25        httr                            CRAN (R 3.6.0) 2019-08-05      1.4.1        1.4.1      OK  
#> 26    jsonlite                            CRAN (R 3.6.0) 2020-02-02      1.6.1        1.6.1      OK  
#> 27       knitr                            CRAN (R 3.6.0) 2020-02-06       1.28         1.28      OK  
#> 28   lifecycle                            CRAN (R 3.6.0) 2020-03-06      0.2.0        0.2.0      OK  
#> 29    magrittr                            CRAN (R 3.6.0) 2014-11-22        1.5          1.5      OK  
#> 30      pillar                            CRAN (R 3.6.2) 2020-05-05      1.4.4        1.4.4      OK  
#> 31       pingr                            CRAN (R 3.6.0) 2019-10-21      2.0.0        2.0.0      OK  
#> 32   pkgconfig                            CRAN (R 3.6.0) 2019-09-22      2.0.3        2.0.3      OK  
#> 33    processx                            CRAN (R 3.6.1) 2020-02-09      3.4.2        3.4.2      OK  
#> 34          R6                            CRAN (R 3.6.0) 2019-11-12      2.4.1        2.4.1      OK  
#> 35     rematch                            CRAN (R 3.6.0) 2016-04-21      1.0.1        1.0.1      OK  
#> 36       rlang                            CRAN (R 3.6.2) 2020-05-02      0.4.6        0.4.6      OK  
#> 37   rprojroot                            CRAN (R 3.6.0) 2018-01-03      1.3-2        1.3-2      OK  
#> 38 sessioninfo                            CRAN (R 3.6.0) 2018-11-05      1.1.1        1.1.1      OK  
#> 39      tibble                            CRAN (R 3.6.2) 2020-04-20      3.0.1        3.0.1      OK  
#> 40   triebeard                            CRAN (R 3.6.0) 2016-08-04      0.3.0        0.3.0      OK  
#> 41        utf8                            CRAN (R 3.6.0) 2018-05-24      1.1.4        1.1.4      OK  
#> 42       vctrs              Github (r-lib/vctrs@504ec96) 2020-06-02      0.3.1        0.3.0      OK *
#> 43      whoami                            CRAN (R 3.6.0) 2019-03-19      1.3.0        1.3.0      OK  
#> 44       withr                            CRAN (R 3.6.0) 2018-03-15      2.1.2        2.2.0      OK *
#> 45        xfun                            CRAN (R 3.6.0) 2020-01-13       0.12         0.14      OK *
#> 46        yaml                            CRAN (R 3.6.0) 2020-02-01      2.2.1        2.2.1      OK  
#> 47 addressable Github (ropenscilabs/addressable@d04bccf) 2020-06-02   0.0.1.91         <NA>    <NA> *
#> 48     cchecks     Github (ropenscilabs/cchecks@df3c80c) 2020-06-02   0.1.8.94         <NA>    <NA> *
#> 49    craninfo                                     local 2020-06-06      0.0.1         <NA>    <NA> *
#> 50   htmltools                            CRAN (R 3.6.0) 2019-10-04      0.4.0         <NA>    <NA> *
```

### Old CRAN release

``` r
craninfo(cran_type = 'oldrel')
#> ── Check Info (Sys.time: 2020-06-06 15:31:59) ───────────────────────────
#> ── Flavor: oldrel-osx-x86_64 ────────────────────────────────────────────
#>        package                                    source       date     loaded cran_version oldrel  
#> 1         Rcpp                            CRAN (R 3.6.3) 2020-04-09    1.0.4.6      1.0.4.6  ERROR  
#> 2    rmarkdown        Github (rstudio/rmarkdown@18ba267) 2020-01-30      2.1.1          2.2  ERROR *
#> 3         curl                            CRAN (R 3.6.0) 2019-12-02        4.3          4.3   NOTE  
#> 4    ipaddress                            CRAN (R 3.6.2) 2020-05-12      0.3.0        0.3.0   NOTE  
#> 5      iptools                            CRAN (R 3.6.0) 2018-12-09      0.6.1        0.6.1   NOTE  
#> 6        readr                            CRAN (R 3.6.0) 2018-12-21      1.3.1        1.3.1   NOTE  
#> 7      stringi                            CRAN (R 3.6.1) 2020-02-17      1.4.6        1.4.6   NOTE  
#> 8      stringr                            CRAN (R 3.6.0) 2019-02-10      1.4.0        1.4.0   NOTE  
#> 9     urltools                            CRAN (R 3.6.0) 2019-04-14      1.7.3        1.7.3   NOTE  
#> 10 AsioHeaders                            CRAN (R 3.6.0) 2020-03-11   1.12.2-1     1.12.2-1     OK  
#> 11  assertthat                            CRAN (R 3.6.0) 2019-03-21      0.2.1        0.2.1     OK  
#> 12   backports                            CRAN (R 3.6.2) 2020-05-13      1.1.7        1.1.7     OK  
#> 13         cli                            CRAN (R 3.6.0) 2020-02-28      2.0.2        2.0.2     OK  
#> 14      crayon                            CRAN (R 3.6.0) 2017-09-16      1.3.4        1.3.4     OK  
#> 15        crul                            CRAN (R 3.6.0) 2019-11-06      0.9.0        0.9.0     OK  
#> 16        desc               Github (r-lib/desc@da19501) 2020-04-03 1.2.0.9000        1.2.0     OK *
#> 17      digest                            CRAN (R 3.6.0) 2020-02-23     0.6.25       0.6.25     OK  
#> 18    ellipsis                            CRAN (R 3.6.2) 2020-05-15      0.3.1        0.3.1     OK  
#> 19    evaluate                            CRAN (R 3.6.0) 2019-05-28       0.14         0.14     OK  
#> 20       fansi                            CRAN (R 3.6.0) 2020-01-08      0.4.1        0.4.1     OK  
#> 21        glue                            CRAN (R 3.6.2) 2020-05-13      1.4.1        1.4.1     OK  
#> 22         hms                            CRAN (R 3.6.0) 2020-01-08      0.5.3        0.5.3     OK  
#> 23    httpcode                            CRAN (R 3.6.2) 2020-04-10      0.3.0        0.3.0     OK  
#> 24        httr                            CRAN (R 3.6.0) 2019-08-05      1.4.1        1.4.1     OK  
#> 25    jsonlite                            CRAN (R 3.6.0) 2020-02-02      1.6.1        1.6.1     OK  
#> 26       knitr                            CRAN (R 3.6.0) 2020-02-06       1.28         1.28     OK  
#> 27   lifecycle                            CRAN (R 3.6.0) 2020-03-06      0.2.0        0.2.0     OK  
#> 28    magrittr                            CRAN (R 3.6.0) 2014-11-22        1.5          1.5     OK  
#> 29      pillar                            CRAN (R 3.6.2) 2020-05-05      1.4.4        1.4.4     OK  
#> 30       pingr                            CRAN (R 3.6.0) 2019-10-21      2.0.0        2.0.0     OK  
#> 31   pkgconfig                            CRAN (R 3.6.0) 2019-09-22      2.0.3        2.0.3     OK  
#> 32    processx                            CRAN (R 3.6.1) 2020-02-09      3.4.2        3.4.2     OK  
#> 33          ps                            CRAN (R 3.6.2) 2020-05-08      1.3.3        1.3.3     OK  
#> 34          R6                            CRAN (R 3.6.0) 2019-11-12      2.4.1        2.4.1     OK  
#> 35     rematch                            CRAN (R 3.6.0) 2016-04-21      1.0.1        1.0.1     OK  
#> 36       rlang                            CRAN (R 3.6.2) 2020-05-02      0.4.6        0.4.6     OK  
#> 37   rprojroot                            CRAN (R 3.6.0) 2018-01-03      1.3-2        1.3-2     OK  
#> 38 sessioninfo                            CRAN (R 3.6.0) 2018-11-05      1.1.1        1.1.1     OK  
#> 39      tibble                            CRAN (R 3.6.2) 2020-04-20      3.0.1        3.0.1     OK  
#> 40   triebeard                            CRAN (R 3.6.0) 2016-08-04      0.3.0        0.3.0     OK  
#> 41        utf8                            CRAN (R 3.6.0) 2018-05-24      1.1.4        1.1.4     OK  
#> 42       vctrs              Github (r-lib/vctrs@504ec96) 2020-06-02      0.3.1        0.3.1     OK  
#> 43      whoami                            CRAN (R 3.6.0) 2019-03-19      1.3.0        1.3.0     OK  
#> 44       withr                            CRAN (R 3.6.0) 2018-03-15      2.1.2        2.2.0     OK *
#> 45        xfun                            CRAN (R 3.6.0) 2020-01-13       0.12         0.14     OK *
#> 46        yaml                            CRAN (R 3.6.0) 2020-02-01      2.2.1        2.2.1     OK  
#> 47 addressable Github (ropenscilabs/addressable@d04bccf) 2020-06-02   0.0.1.91         <NA>   <NA> *
#> 48     cchecks     Github (ropenscilabs/cchecks@df3c80c) 2020-06-02   0.1.8.94         <NA>   <NA> *
#> 49    craninfo                                     local 2020-06-06      0.0.1         <NA>   <NA> *
#> 50   htmltools                            CRAN (R 3.6.0) 2019-10-04      0.4.0         <NA>   <NA> *
```
