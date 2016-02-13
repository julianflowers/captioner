<!-- README.md is generated from README.Rmd. Please edit that file -->
[![Build Status](https://travis-ci.org/adletaw/captioner.png?branch=master)](https://travis-ci.org/adletaw/captioner) [![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/captioner)](http://cran.r-project.org/package=captioner) [![Coverage Status](https://coveralls.io/repos/adletaw/captioner/badge.svg?branch=master&service=github)](https://coveralls.io/github/adletaw/captioner?branch=master)

*captioner* is an R package for generating figure numbers and captions

Installation
============

*captioner* is now available on [CRAN](https://cran.r-project.org/web/packages/captioner/index.html). If you would like to install the current development version:

-   `install.packages("devtools")`
-   `devtools::install_github("adletaw/captioner")`

or if you want the vignette:

-   `devtools::install_github("adletaw/captioner", build_vignettes = TRUE)`
-   `vignette("using_captioner")`

Basic Usage
===========

A call to the function `captioner()` returns a captioner function for each set of figures, tables, etc. that you want to create.

You can generate a full caption:

``` r
fig_nums <- captioner()
fig_nums("my_pretty_figure", "My pretty figure's caption.")
#> [1] "Figure  1: My pretty figure's caption."
```

You can also generate a figure reference:

``` r
fig_nums("my_pretty_figure", display = "cite")
#> [1] "Figure  1"
```

Which can be displayed inline using inline code chunks, like so (Figure 1).

You can also store the caption and use it in your R code chunk in markdown documents:

``` r
my_first_caption <- fig_nums("my_other_figure", "My other figure's caption.")
```

``` r
plot(cars)
```

![](README-ex_3b-1.png)<!-- -->

``` r
my_first_caption
#> [1] "Figure  2: My other figure's caption."
```

If you create a new set of captions, perhaps for your tables, the numbering restarts:

``` r
table_nums <- captioner(prefix = "Table")
table_nums("cat_table", "A table of cat breeds.")
#> [1] "Table  1: A table of cat breeds."
```

You can abbreviate in text citations by using `partial`<sup>1</sup> from the package `pryr` to create a shorter version of the function. For example:

``` r
citef <- pryr::partial(fig_nums, display = "cite")
citef("my_pretty_figure")
#> [1] "Figure  1"
```

Take a look at the [vignette](https://github.com/adletaw/captioner/tree/master/vignettes/using_captioner.Rmd) for many more details.

------------------------------------------------------------------------

1.  I learned this from the glorious H Wickham and [you can too](http://adv-r.had.co.nz/)
