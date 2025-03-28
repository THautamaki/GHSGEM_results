
# Results of the article: Gene co-expression network estimation using GEM with GHS prior

This repository contains all codes and results files used to produce the
results for the article *Gene co-expression network estimation using
generalized expectation-maximization algorithm with graphical horseshoe
prior*.

We implemented our method in the R package called GHSGEM, which is
available on GitHub at <https://github.com/THautamaki/GHSGEM>.

## Original MATLAB codes

The original MATLAB codes of the GHS Gibbs sampler (GHS MCMC), GHS local
linear approximation (GHS LLA), GHS-like expectation conditional
maximization (GHS-like ECM or HSL ECM), and GHS-like MCMC (or HSL MCMC)
methods can be found on the following GitHub pages:

- <https://github.com/liyf1988/GHS>
  - Author: Yunfan Li
- <https://github.com/sagarknk/GHS-LLA-codes>
  - Author: Ksheera Sagar K. N., Purdue University
  - Codes were modified and redistributed with his permission.
- <https://github.com/sagarknk/Graphical_HSL>
  - Author: Ksheera Sagar K. N., Purdue University
  - Codes were modified and redistributed with his permission.

## Real-world datasets

The CEU dataset is available on Sanger Institute’s website:
<https://ftp.sanger.ac.uk/pub/genevar>, and the DLBC dataset is
available on the website of the PRECISE framework:
<https://mjha.shinyapps.io/PRECISE>.

## Structure of the repository

The files in the repository are organized in the main directories as
follows:

- Data
  - This directory is not stored in GitHub as simulated datasets can be
    generated anytime, and real-world datasets are available publicly on
    the Internet. The R code creates this when simulated datasets are
    generated. Please store the real-world datasets in the directories
    named `CEU_dataset` and `DLBC_dataset`.
- Figures
  - Contains all figures generated for the main article and
    supplementary material in own directories.
- MATLAB_files
  - The root contains some helper functions.
  - Each method has its directories where associated codes are.
  - Both real-world datasets also have their directories where all
    MATLAB codes needed to analyse the datasets are stored.
- R_files
  - Contains all codes used in the R.
- Results_files
  - The root contains the total times of the MATLAB methods.
  - The simulations with both problem dimensions $p = \{100, 200\}$ have
    their directories, where results are stored per method per
    directory.
  - Both real-world datasets have their directories containing all
    results files.

## Performing the simulation analyses

> [!IMPORTANT]
> All provided scripts assume the working directory has
> the same directory structure as this repository. The scripts use
> relative paths to read and save files.

The simulated datasets used in the article can always be created using
the function `generate_datasets()` without arguments (the default
arguments). It saves datasets in the `Data` directory in Rds and
csv-format for R and MATLAB use, respectively.

To run analyses using R methods, we created an R script named
`Run_simulations_R_methods_and_combine_results.R` which serves as the
main file for the simulation analysis. It has been well commented on, so
we will not provide details here. It installs all necessary R packages,
creates simulated datasets, runs R methods, combines all result files,
and finally prints the results.

Each MATLAB method has `<method_name>_analysis.m` file to run
simulations. They are all well-commented and can be run using MATLAB’s
`Run all sections` shortcut. Note that the helper functions should be
placed into the `%userprofile%\Documents\MATLAB` folder (if a Windows
machine) so that MATLAB can find them. The simulation results have
run-to-run variance as we do not use fixed seeds for every MATLAB method
(and StARS for GLASSO). The biggest difference in MCC we saw was about
0.012.

> [!CAUTION]
> Please note that if a similar system is used, as
> described in the article (a 16-core AMD Ryzen 9 7950X3D processor and
> 64 GB of RAM), all simulations require approximately 3.5 days to
> complete.

## Performing the real-world dataset analyses

### The CEU dataset

We created R and MATLAB scripts to perform analyses of the CEU dataset.
We suggest creating transformed datasets first by running lines 7–32
from the R script `Analysis_of_CEU_dataset.R`. Then, MATLAB methods can
be run from the script `Run_CEU_dataset_MATLAB_methods.m` using MATLAB’s
`Run all sections` shortcut. Finally, the remaining lines from the R
script can be executed. It performs the GHS GEM method, calculates the
numbers used in the article, and plots the estimated networks.

### The DLBC dataset

We created R and MATLAB scripts to perform analyses of the DLBC dataset.
We suggest creating transformed datasets first by running lines 8–32
from the R script `Analysis_of_DLBC_dataset.R`. Then, MATLAB methods can
be run from the script `Run_DLBC_dataset_MATLAB_methods.m` using
MATLAB’s `Run all sections` shortcut. Finally, the remaining lines from
the R script can be executed. It performs the GHS GEM method, calculates
the numbers used in the article, and plots the estimated networks.

## Supplementary materials

### Analysis of the kappa threshold

Supplementary Figures S1, S2, and S3 can be created using the R script
`Analysis_of_kappa_threshold.R`.

### Analysis of the initial values of the GHS GEM algorithm

Analysis of the initial values of the GHS GEM algorithm, as presented in
the supplementary material, can be performed using the R script
`Analysis_of_initial_values.R` (Supplementary Table S1). Please note
that the analysis requires about 3 hours to complete, assuming a system
with similar specifications is used, as described above.

### Parameter c in the global scale parameter formula

Supplementary Figure S4 can be created using the R script
`Analysis_of_c_parameter.R`. Please note that the analysis requires
approximately 5 hours to complete, assuming a system with similar
specifications is used, as described above.

### Results with the fastGHS method

We did not include the fastGHS method results in the main article, but
they can be reproduced using the same R script used for the main results
(`Run_R_methods_and_combine_results.R`, lines from 102 forward). The
script contains code to create Supplementary Tables S2 and S3. We also
did some additional analysis, which can be reproduced using the R script
`Additional_fastGHS_analysis.R` (Supplementary Figures S5 and S6).
