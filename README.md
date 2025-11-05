# bayesintro

An R package for teaching Bayesian inference to PhD students, featuring comprehensive examples with epidemiological models.

## Overview

This package provides educational materials for an introductory course on Bayesian statistics. The main vignette demonstrates a complete Bayesian workflow using an **SIR (Susceptible-Infected-Recovered) epidemic model**.

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

## Background

Intro to Bayes theory

* 

## "Author

Created for the CCHG PhD student Bayesian inference course.
