# CONTRIBUTING.md

## Package structure

Kaphi is an R package.  As a result, the directory is structured according to the requirements of an R package distribution with the following subdirectories and files:
* R - contains R code (with extension `.R`) that implements package-specific functions to be called from R.
* src - contains source and header files for compiled code, such as C.
* tests - contains R scripts that implement unit tests of the package.
* DESCRIPTION - a file that contains basic information about the package.  This is a required file for R to recognize this as a valid package at installation.
* NAMESPACE


## Prerequisites

To contribute to the development of Kaphi, you will need to install the following libraries:

* [R libraries](https://cran.r-project.org/)
* [igraph C library](http://igraph.org/c/) modified by @rmcclosk, included in package subfolder `\src`
* [GNU Standard Library](https://www.gnu.org/software/gsl/)
* [Judy](https://sourceforge.net/projects/judy/)
* [check](https://libcheck.github.io/check/)
* [GNU bison](https://www.gnu.org/software/bison/), version >=3.0.4
* [GNU flex](https://github.com/westes/flex)


## Writing a C extension function

To add a function in C that is callable from R, you need to write the function in a source file in the `src` directory that includes the following include statements:
```
#define USE_RINTERNALS
#include <R.h>
#include <Rinternals.h>
```
Next, you need to provide a means of calling the C function from an R script in the `/R` subdirectory:
```
node.count <- function(tree) {
    res <- .Call("R_Kaphi_nodecount", tree, PACKAGE="Kaphi")
    res
}
```
and modify the `NAMESPACE` file so that this R function is exported with the package contents:
```
export(node.count)
```
