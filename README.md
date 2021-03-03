# Rcplex2

This R package modifies the original Rcplex 0.3-3 package from CRAN, with added functionality.

Changes to the original package include:
  1. Enable specifying the number of threads to use and parallel mode (opportunistic or deterministic);
  2. Enable warm start (i.e. providing an inition solution);
  3. Changed the default values of some of the parameters;
  4. Changed package name to Rcplex2 to avoid conflict if Rcplex is installed;
  5. Enable specifying the "Optimality Target" parameter for QP.

Changed parts in the codes are marked by comments.


## Install

Please first install the IBM ILOG CPLEX Optimization Studio, you can get a free academic version from the official IBM website.

Clone this git repo:
```
git clone https://github.com/ImNotaGit/Rcplex2.git
```

Compress the repo into a .tar.gz file:
```
tar czf Rcplex2.tar.gz Rcplex2
```

Then use the command below to install. Replace `${cplex_dir}` with the installation directory of CPLEX, e.g. something like `$HOME/ibm/ILOG/CPLEX_Studio1210`

```
R CMD INSTALL --configure-args="PKG_CFLAGS='-fPIC -m64 -fno-strict-aliasing' \
    PKG_CPPFLAGS=-I${cplex_dir}/cplex/include \
    PKG_LIBS='-L${cplex_dir}/cplex/lib/x86-64_linux/static_pic \
    -lcplex -lm -lpthread'" Rcplex2.tar.gz
```

Note: The original configure file is not perfect, as a result this package may be hard to install. I changed the configure file in a dirty way to circumvent an issue related to `CPXversion` (basically I set the value of the variable `ac_cv_search_CPXversion` to `"none required"` by default), which worked for me but may have side effects on other systems. The original configure file was saved as configure.bak.
