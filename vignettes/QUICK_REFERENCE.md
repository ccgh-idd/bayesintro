# Bayesian Inference Quick Reference Card

*Print this for quick reference during the course!*

## Key Concepts

### Bayes' Theorem

```
Posterior ∝ Likelihood × Prior

p(θ|data) ∝ p(data|θ) × p(θ)
```

**In words**: What we believe about parameters after seeing data is proportional to how likely the data are given parameters, times what we believed before.

### Components of Bayesian Analysis

1. **Prior**: p(θ) - What we believe before seeing data
2. **Likelihood**: p(data|θ) - How data are generated given parameters
3. **Posterior**: p(θ|data) - What we believe after seeing data
4. **Posterior Predictive**: p(new_data|data) - Predictions with uncertainty

## SIR Model Equations

```
dS/dt = -β × S × I / N
dI/dt = β × S × I / N - γ × I  
dR/dt = γ × I
```

**Parameters:**

- β: transmission rate (new infections per infected per day)
- γ: recovery rate (1/infectious period)
- R₀ = β/γ: basic reproductive number

## MCMC Convergence Diagnostics

### What to Check

| Diagnostic            | Good              | Bad           | Action if Bad                |
| --------------------- | ----------------- | ------------- | ---------------------------- |
| **Rhat**        | < 1.01            | > 1.1         | Run longer, check model      |
| **ESS**         | > 400             | < 100         | Run longer, tune sampler     |
| **Trace plots** | Fuzzy caterpillar | Trends, stuck | Check initialization, tune   |
| **Chains**      | All overlap       | Separated     | Run longer, different starts |

### Rhat (Gelman-Rubin Statistic)

- Compares within-chain vs. between-chain variance
- **< 1.01**: Excellent convergence ✓
- **1.01-1.05**: Good convergence
- **1.05-1.1**: Marginal - run longer
- **> 1.1**: Not converged - investigate!

### Effective Sample Size (ESS)

- Number of "independent" samples from posterior
- **ESS > 400**: Good for most purposes
- **ESS > 1000**: Excellent
- **ESS < 100**: Too low - run longer or tune sampler

## Reading Trace Plots

**Good trace plot (converged):**

```
Chain 1:  ~~~~~~~~~~~~~~~~
Chain 2:  ~~~~~~~~~~~~~~~~  
Chain 3:  ~~~~~~~~~~~~~~~~
        (fuzzy caterpillar, all chains overlap)
```

**Bad trace plot (not converged):**

```
Chain 1:  ------________
Chain 2:  ___________----
Chain 3:  ----___________
        (trends, separation, stuck values)
```

## Interpreting Results

### Credible Intervals (CI)

**95% CI: [0.35, 0.45] for β**

Interpretation: "There is a 95% probability that β lies between 0.35 and 0.45 given the data and model."

**NOT**: "95% of the time, the true value is in this interval" (that's frequentist!)

### Posterior Predictive Checks

**Good fit:**

- Observed data falls within 80-95% predictive intervals
- Predicted and observed distributions overlap
- No systematic patterns in residuals

**Poor fit:**

- Many observations outside intervals
- Predicted distribution very different from observed
- Systematic patterns (model missing something)

## Common Priors

### Weakly Informative

```r
beta ~ Normal(0.4, 0.2)   # Centers prior, allows data to dominate
gamma ~ Normal(0.1, 0.05)
```

### Uniform (Non-informative)

```r
beta ~ Uniform(0, 1)      # All values equally likely
gamma ~ Uniform(0, 1)
```

### Informative

```r
beta ~ Normal(0.4, 0.05)  # Strong prior belief
gamma ~ Normal(0.1, 0.01)
```

## MCMC Sampler Comparison

| Sampler              | Speed   | Ease of Use | When to Use                |
| -------------------- | ------- | ----------- | -------------------------- |
| **Metropolis** | Slow    | Simple      | Learning, simple models    |
| **DEzs**       | Fast    | Easy        | Default choice             |
| **DREAM**      | Fast    | Easy        | Multimodal posteriors      |
| **HMC (Stan)** | Fastest | Moderate    | Complex models, production |

## R Code Snippets

### Load Packages

```r
# BayesianTools approach
library(BayesianTools)
library(deSolve)
library(ggplot2)

# Stan approach  
library(rstan)
library(bayesplot)
```

### Check Convergence

```r
# BayesianTools
summary(fit)
gelmanDiagnostics(fit)
plot(fit)

# Stan
print(fit, pars = c("beta", "gamma"))
traceplot(fit)
```

### Extract Samples

```r
# BayesianTools
samples <- getSample(fit)
beta_post <- samples[, 1]

# Stan
samples <- extract(fit)
beta_post <- samples$beta
```

### Calculate Credible Intervals

```r
# 95% CI
quantile(beta_post, c(0.025, 0.975))

# 80% CI
quantile(beta_post, c(0.1, 0.9))

# Mean and SD
mean(beta_post)
sd(beta_post)
```

## Troubleshooting

### Model Won't Converge

1. Run more iterations
2. Check for coding errors
3. Try different starting values
4. Use stronger priors (but carefully!)
5. Check if model is identifiable

### Code is Slow

1. Reduce number of time points
2. Use coarser time steps
3. Reduce number of iterations (after convergence)
4. Use parallel chains
5. Consider Stan (faster for complex models)

### Posterior is Weird

1. Check likelihood function for bugs
2. Verify prior makes sense
3. Look at data - any issues?
4. Try simpler model first
5. Plot prior predictive distribution

## Reporting Results

### Parameter Estimates

```
β = 0.40 (95% CI: 0.35-0.45)
γ = 0.10 (95% CI: 0.08-0.12)
R₀ = 4.0 (95% CI: 3.2-5.0)
```

### Model Fit

- "The model provided good fit to the data, with 94% of observed points falling within the 95% posterior predictive interval."
- Include posterior predictive check plot

### Convergence

- "All chains converged successfully (Rhat < 1.01 for all parameters)."
- "Effective sample sizes exceeded 1000 for all parameters."
