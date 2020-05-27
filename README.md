# Rcplex2

This R package modifies the original Rcplex 0.3-3 package from CRAN, with added functionality.

Changes to the original package include:
  1. Enable specifying the number of threads to use and parallel mode (opportunistic or deterministic);
  2. Enable warm start (i.e. providing an inition solution);
  3. Changed the default values of some of the parameters;
  4. Changed package name to Rcplex2 to avoid conflict if Rcplex is installed.

Changed parts in the codes are marked by comments.


## Install

Please first install the IBM ILOG CPLEX Optimization Studio, you can get a free academic version from the official IBM website.

Clone this git repo:
```
git clone https://github.com/ruppinlab/Rcplex2.git
```

Then use a command in the form of `R CMD INSTALL --configure-args="PKG_CFLAGS='AAA' PKG_CPPFLAGS=BBB PKG_LIBS='CCC'" Rcplex2` to install, where AAA, BBB and CCC are determined by the variables `CFLAGS` and `CLNFLAGS` in the file \<cplex_dir\>/cplex/examples/\<system\>/\<libformat\>/Makefile. Specifically, BBB is the last term in `CFLAGS`, AAA are the terms excluding the last in `CFLAGS` (in that order), and CCC are `-L$(CPLEXLIBDIR)` plus all the terms in `CLNFLAGS`. For more system-specific details, see the inst/INSTALL file.

Below is an example for installation on a 64-bit Linux system. Replace `${cplex_dir}` with the installation directory of CPLEX, e.g. something like `$HOME/ibm/ILOG/CPLEX_Studio1210`. This example worked for me on Biowulf.

```
R CMD INSTALL --configure-args="PKG_CFLAGS='-fPIC -m64 -fno-strict-aliasing' \
    PKG_CPPFLAGS=-I${cplex_dir}/cplex/include \
    PKG_LIBS='-L${cplex_dir}/cplex/lib/x86-64_linux/static_pic \
    -lcplex -lm -lpthread'" Rcplex2
```

On MacOS, the CPLEX installation directory `${cplex_dir}` can be something like `/Applications/CPLEX_Studio1210`; also need to change the `${cplex_dir}/cplex/lib/x86-64_linux/static_pic` to something like `${cplex_dir}/cplex/lib/x86-64_osx/static_pic`.

Note: In some cases, there may be an issue related to `CPXversion` that prevents successful installation. I changed the configure file in a dirty way to circumvent this issue (basically I set the value of the variable `ac_cv_search_CPXversion` to `"none required"` by default), which worked for me but may have side effects in other cases. The original configure file was saved as configure.bak.
