# Rcplex2
Adding minor functions to the Rcplex package.

I made the following changes to the original Rcplex 0.3-3 package from CRAN:
  1. Enable specifying the number of threads to use and parallel mode (opportunistic or deterministic);
  2. Enable warm start (i.e. providing an inition solution);
  3. Changed the default values of some of the parameters;
  4. Changed package name to Rcplex2 to avoid conflict if Rcplex is installed.

Changed parts in the codes are marked by comments.
