# ds-cleaningmodel

## Introduction

This reposotory hosts a notebook and comments about how to qualify losses from a manufacturing site, including assessing historical data, and determining how to define a point when remedial actions should be instigated.

## Instructions

To use the notebook as intended:
1) Populate the `Data/` directory with the requisite CSV data file.
2) Update the `config.yml` with an appropriate section tagged with your R username (`Sys.info()['user']`), and provision the `wd` parameter to the root directory of this repository.
3) Open and run the `CleaningModelEDA.Rmd` R notebook. It is possible you may require additional packages to be installed.

## Approach explanation

For this problem, it was important to assess how the two data feeds were distributed, and the character of their relation. The business-critical values are given by the product of the two data as units per time, and hence it also became relevant to identify which portions of the data to use for defining a measurement basis, and which portions would be inappropriate to include as they may bias any solution.

Minor to moderate issues were present with some of the data, with both partial and full rows missing; partially incomplete rows were imputed with the appropriate median, whereas fully absent rows were assumed as 0. It would be valuable to understand why complete rows were absent, particularly in one case of up to 96 hours of contiguous observations missing, not at random. Having imputed and combined the two data streams to give quantities estimated per day, the behaviour over time was assessed, and three anomalous time segments omitted from the establishment of a reference distribution.

A method to qualify a day's total losses in relation to this reference distribution is provided in an R function, `fn_lossRag()`, which returns a text string identifying if within normal bounds, approaching bounds, or exceeding acceptable values.
