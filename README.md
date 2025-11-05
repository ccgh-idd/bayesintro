# bayesintro

An R package for teaching Bayesian inference to PhD students, featuring comprehensive examples with epidemiological models.

## Overview

This package provides educational materials for an introductory course on Bayesian statistics. The main vignette demonstrates a complete Bayesian workflow using an **SIR (Susceptible-Infected-Recovered) epidemic model**.

## Background

Introduction to MCMC

* [The Strange Math That Predicts (Almost) Anything](https://www.youtube.com/watch?v=KZeIEiBrT_w) <- really good Veritasium vide on Markov chains
* [Markov Chain Monte Carlo (MCMC) : Data Science Concepts](https://www.youtube.com/watch?v=yApmR-c_hKU) <- Good gentle introduction to MCMC
* [MCMC &amp; the art of Sampling without Sampling](https://medium.com/data-science-collective/mcmc-the-art-of-sampling-without-sampling-7272697e5744) <- comprehensive, but a bit heavy, overview of MCMC

Books on MCMC

* **"Statistical Rethinking" by Richard McElreath (2nd edition, 2020).** This is widely considered the best modern introduction.
* *A Student’s Guide to Bayesian Statistics by Ben Lambert.** Not quite as popular as Richard's, but very comprehensive for beginners.
* **"Bayesian Data Analysis" by Gelman, Carlin, Stern, Dunson, Vehtari & Rubin (3rd edition, 2013).** The definitive comprehensive textbook.

## What You'll Learn

- **Bayesian fundamentals**: Priors, likelihoods, and posterior distributions
- **MCMC methods**: Hamiltonian Monte Carlo with Stan
- **Model checking**: Convergence diagnostics and posterior predictive checks
- **Practical workflow**: From data simulation to forecasting
- **Uncertainty quantification**: Credible intervals and predictive distributions

## Installation

```r
# Install from local directory
devtools::install_github("yourusername/bayesintro", build_vignettes = TRUE)

# Or install locally with vignettes
devtools::install(build_vignettes = TRUE)
```

## Quick Start

```r
# View available vignettes
vignette(package = "bayesintro")

# Stan-based vignette (requires C++ compiler)
vignette("sir_model_bayesian_inference", package = "bayesintro")

# BayesianTools vignette (pure R, easier setup!)
vignette("sir_model_bayesiantools", package = "bayesintro")
```

## Prerequisites

Students should have:

- Basic R programming knowledge
- Familiarity with probability distributions
- Understanding of likelihood functions (helpful but not required)

No prior knowledge of Bayesian statistics or Stan is required!

## Course Structure

We provide **two complementary vignettes** covering the same SIR model with different tools:

### Vignette 1: BayesianTools Approach

Using `BayesianTools` - pure R, no compilation required!

1. Same SIR model and data simulation
2. Likelihood and prior functions in pure R
3. Multiple MCMC algorithms (DEzs, DREAM, Metropolis)
4. Comparison of different samplers
5. Same diagnostic and validation workflow
6. Easier setup for beginners

## Dependencies

Main packages used:

- `ggplot2`: Data visualization
- `bayesplot`: MCMC diagnostics and visualization
- `deSolve`: Solving differential equations

See `DESCRIPTION` for the complete list.
