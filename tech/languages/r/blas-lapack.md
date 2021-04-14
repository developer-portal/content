---
title: BLAS/LAPACK switching
subsection: r
order: 3
---

# BLAS/LAPACK switching

Since Fedora 33, R is linked against [FlexiBLAS](https://www.mpi-magdeburg.mpg.de/projects/flexiblas), a BLAS/LAPACK wrapper library that enables runtime switching of the optimized backend.

## Installation

The accompanying `R-flexiblas` package enables BLAS/LAPACK switching without leaving the R session, as well as setting the number of threads for parallel backends.

```bash
$ sudo dnf install R-flexiblas # install FlexiBLAS API interface for R
$ sudo dnf install flexiblas-* # install all available optimized backends
```

## Usage

Then, in an R session we see:

```r
library(flexiblas)

# check whether FlexiBLAS is available
flexiblas_avail()
#> [1] TRUE

# get the current backend
flexiblas_current_backend()
#> [1] "OPENBLAS-OPENMP"

# list all available backends
flexiblas_list()
#> [1] "NETLIB"           "__FALLBACK__"     "BLIS-THREADS"     "OPENBLAS-OPENMP"
#> [5] "BLIS-SERIAL"      "ATLAS"            "OPENBLAS-SERIAL"  "OPENBLAS-THREADS"
#> [9] "BLIS-OPENMP"

# set/get the number of threads
flexiblas_set_num_threads(12)
flexiblas_get_num_threads()
#> [1] 12
```

## Benchmarking example

This is an example of GEMM benchmark for all the backends available.
You can run the following code interactively or as a script file.

```r
library(flexiblas)

n <- 2000
runs <- 10
ignore <- "__FALLBACK__"

A <- matrix(runif(n*n), nrow=n)
B <- matrix(runif(n*n), nrow=n)

# load backends
backends <- setdiff(flexiblas_list(), ignore)
idx <- flexiblas_load_backend(backends)

# benchmark
timings <- sapply(idx, function(i) {
  flexiblas_switch(i)

  # warm-up
  C <- A[1:100, 1:100] %*% B[1:100, 1:100]

  unname(system.time({
    for (j in seq_len(runs))
      C <- A %*% B
  })[3])
})

results <- data.frame(
  backend = backends,
  `timing [s]` = timings,
  `performance [GFlops]` = (2 * (n / 1000)^3) / timings,
  check.names = FALSE)

results[order(results$performance),]
#>            backend timing [s] performance [GFlops]
#> 1           NETLIB     56.776            0.2818092
#> 5            ATLAS      5.988            2.6720107
#> 2     BLIS-THREADS      3.442            4.6484602
#> 8      BLIS-OPENMP      3.408            4.6948357
#> 4      BLIS-SERIAL      3.395            4.7128130
#> 6  OPENBLAS-SERIAL      3.206            4.9906425
#> 7 OPENBLAS-THREADS      0.773           20.6985770
#> 3  OPENBLAS-OPENMP      0.761           21.0249671
```

## References

- [FlexiBLAS as BLAS/LAPACK manager](https://fedoraproject.org/wiki/Changes/FlexiBLAS_as_BLAS/LAPACK_manager)
- [Upstream documentation](https://github.com/Enchufa2/r-flexiblas)
