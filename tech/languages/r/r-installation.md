---
title: R
subsection: r
section: tech-languages
order: 1
version: 4.0.0
description: Free software environment for statistical computing and graphics.
---

# R in Fedora

[R](https://www.r-project.org/) provides a wide variety of statistical and graphical techniques:
linear and nonlinear modelling, statistical tests, time series analysis, classification, clustering, and much more through its rich package ecosystem.

## Installation

The newest R release, including recommended packages and development headers and tools, can be installed by running:

```bash
$ sudo dnf install R
```

The following components will be installed by default:

| Component      | Description                                                 |
|----------------|-------------------------------------------------------------|
| R-core         | The minimal R components necessary for a functional runtime |
| R-core-devel   | Core files for development of R packages (no Java)          |
| R-java         | R with Fedora-provided Java Runtime Environment             |
| R-java-devel   | Development package for use with Java enabled R components  |
| libRmath       | Standalone math library from the R project                  |
| libRmath-devel | Headers from the R standalone math library                  |

## Running R

To run R, simply type `R` in your terminal:

```bash
$ R
R version 4.0.4 (2021-02-15) -- "Lost Library Book"
Copyright (C) 2021 The R Foundation for Statistical Computing
Platform: x86_64-redhat-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

>
```

Now you can start to write in R! Let's print _Hello World_!

```r
print("Hello World!")
```

If you want to **exit** R, type `quit()` or press `Ctrl` + `D`, then press `n` to avoid saving the workspace.

To run a program written in R, type `Rscript` followed by the path and name of the program.
For example, for a script called `example.R` in the current path, run the following:

```bash
$ Rscript example.R
```

## What next?

* [R Project homepage](https://www.r-project.org/)
* [R Manuals](https://cran.r-project.org/manuals.html)
* [R for Data Science](https://r4ds.had.co.nz/), by Hadley Wickham.
* [Advanced R](https://adv-r.hadley.nz/), by Hadley Wickham.
