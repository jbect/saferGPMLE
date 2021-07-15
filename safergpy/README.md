# saferGPMLE/safergpy

## What you will find in here

This directory provides a framework for producing the other results of
  the article, and in particular the results presented in Section 5.

## Table of contents

  * [Datasets](#datasets)
  * [Benchmarks](#benchmarks)
  * [Running a benchmark](#running-a-benchmark)
  * [Reports](#reports)

## Datasets

All the datasets used for experiments are located under `./datasets`, divided
in two subdirectories: `/single_doe` and `/repetitions`.

Inside `/single_doe`, corresponding to each of the following test functions
(input dimension d) we have four datasets of sizes 3d, 5d, 10d and 20d, respectively.

  * Branin function (d=2)
  * Borehole function (d=8)
  * WeldedBeam Design function (d=4)
  * g10 function (d=8)
  * g10mod function (d=8)
  * g10modmod function (d=8)

Inside `/repetitions`, we have the datasets corresponding to the third benchmark
described below.

## Benchmarks

### First benchmark

For each dataset, find the MLE for the constant-mean Matérn-5/2 anisotropic
model.

The results for this benchmark are stored in the folder `./results/bench1`.

### Second benchmark

For each n-dataset, find the MLE for each possible (n-1)-dataset that can be
extracted from it.

Same model as in the first benchmark.

The results for this benchmark are stored in the folder `./results/bench2`.

### Third benchmark

For reproducing the results in Table 2 of the article, the second
benchmark is repeated with 50 different datasets of sizes 3d=24 and
5d=40 respectively, for the Borehole function (d=8).

The datasets are located in `./datasets/repetitions`

The results for this benchmark are stored in the folder `./results/bench2_repetition`.

## Running a benchmark

Syntax:
```
export OMP_NUM_THREADS=1  # recommended
python3 code/bench/py/launcher.py type i input_data_path output_data_path informations
```

Example:
```
python3 code/bench/py/launcher.py simple 001 datasets/single_doe results/bench1/data
```

Input arguments explained:
* `type`: indicates whether you want to test estimation on each
  dataset (i.e. 'simple') or on each of the (n-1) datasets obtained by
  removing one point from the original dataset (i.e. 'loo').
* `i`: index of the method you want to test.
* `intput_data_path`: folder where the datasets are stored.
* `output_data_path`: folder where you want to write the results.
* `informations`: optional, could be provided to specify BLAH2 (see
  Methods names and numbers section).

## Reports

### Plotting empirical CDFs of NLL differences

You can plot the empirical CDF of the NLL differences between the
results of one method and the best known values.

The script is `./code/report/plot_error_cdf_benchmark.py` and can be
used like this :

```
python3 plot_error_cdf_benchmark.py --solid-lines gpy_mle0121 gpy_mle0122 --dashed-lines gpy_mle0131 gpy_mle0132
```

The script fails if the methods have not been run on the exact
same collection of datasets.

### Reproducing the figures from the article

More details in [`code/report/README.md`](./code/report/README.md).
