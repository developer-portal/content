---
title: R packages
subsection: r
order: 2
---

# Installing packages

Recommended R packages are included as part of the R installation.
A number of popular add-on packages from [CRAN](https://cran.r-project.org/), [Bioconductor](https://bioconductor.org/) and other sources are readily available via the Fedora repositories.
They are named with an `R-` prefix, such as `R-ggplot2`.
To install a package, run:

```bash
$ sudo dnf install R-ggplot2
```

The following command:

```bash
$ sudo dnf repoquery --repo=fedora-source 'R-*'
```

provides a list of all R packages in Fedora.

## Installation from source

If you have the [R package installed](/tech/languages/r/r-installation.html), thousands of additional add-on packages can be installed from the official CRAN and Bioconductor repositories.
To install e.g. the `ggplot2` package from source, open the _R console_ and run:

```r
install.packages("ggplot2")
```

With this method, packages are installed into the user home directory, under `~/R`.

See also the [`remotes`](https://remotes.r-lib.org/) package, to learn how to install packages from a variety of sources (e.g., GitHub),
and the [`renv`](https://rstudio.github.io/renv/) package, to learn how to manage environments and to install specific versions of packages.

## Additional binary packages

The [cran2copr](https://copr.fedorainfracloud.org/coprs/iucar/cran/) project maintains binary RPM contributed repositories for the current and previous stable Fedora version for most of CRAN (~17k packages as of Apr 2021) in an automated way using [Fedora Copr](https://copr.fedorainfracloud.org/).
These repositories are automatically synchronized with CRAN on a daily basis.
To ensure compatibility with the official Fedora repository, these set of packages are named with the `R-CRAN-` prefix (`R-CRAN-ggplot2` for example), and are installed into `/usr/local/lib/R/library`.

To enable this Copr repository in your system:

```bash
$ sudo dnf install 'dnf-command(copr)'
$ sudo dnf copr enable iucar/cran
```

For integrating binary package installation into your R session, you can install `R-CoprManager`:

```bash
$ sudo dnf install R-CoprManager
```

With `CoprManager`, the Copr `iucar/cran` repository will be used when installing from the R console:

```r
install.packages("car")
```

If a package is not available, then it just falls back to source installation from CRAN.

On the other hand, `remove.packages` will still remove only packages installed in your user library.
If you want to remove system packages, run:

```r
CoprManager::remove_copr("car")
```

If you want to disable the `CoprManager`, so that `install.packages` only works from source again, then run:

```r
CoprManager::disable()
install.packages("car")
```
