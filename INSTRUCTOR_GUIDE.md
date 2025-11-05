# Instructor Guide: Bayesian Inference Course

## Package Overview

This R package provides comprehensive teaching materials for an introductory Bayesian inference course using SIR epidemic models. It includes **two parallel implementations** to accommodate different learning styles and technical constraints.

## Course Structure

### Recommended Teaching Sequence

**Option 1: BayesianTools Only (Recommended for most students)**

- Session 1 (2-3 hours): `sir_model_bayesiantools.Rmd`
- Covers all Bayesian fundamentals without C++ compilation
- Students see full likelihood and prior functions in R
- Can compare multiple MCMC algorithms

**Option 2: Both Tools (For advanced students)**

- Session 1 (2 hours): `sir_model_bayesiantools.Rmd`
- Session 2 (2 hours): `sir_model_bayesian_inference.Rmd`
- Allows comparison of tools and deeper understanding
- Prepares students for professional research

## Pre-Course Setup

### For Students: Setup Checklist

Send this to students **at least 1 week before the course**:

#### Minimum Setup (BayesianTools):

```r
install.packages(c(
  "BayesianTools",
  "coda", 
  "deSolve",
  "ggplot2",
  "dplyr",
  "tidyr",
  "knitr",
  "rmarkdown"
))
```

#### Full Setup (Including Stan):

```r
# First install BayesianTools packages (above)

# Then install Stan (requires C++ compiler)
install.packages("rstan", dependencies = TRUE)

# Test Stan installation
example(stan_model, package = "rstan", run.dontrun = TRUE)
```

**Note**: Stan installation can be problematic. Have a backup plan using only BayesianTools!

## During the Course

### Session Plan (BayesianTools Vignette)

**Part 1: Introduction (30 min)**

- Motivation for Bayesian inference
- SIR model overview
- Why epidemiological models?

**Part 2: Data and Model (45 min)**

- Simulate epidemic data
- Define likelihood function (line by line!)
- Specify prior distributions
- Discussion: How do we choose priors?

**Break (10 min)**

**Part 3: Fitting (30 min)**

- Run MCMC algorithms
- Watch live sampling
- Compare different samplers (DEzs, DREAM, Metropolis)

**Part 4: Diagnostics (30 min)**

- Trace plots - what to look for
- Rhat and effective sample size
- Convergence discussion
- Common problems and solutions

**Part 5: Validation and Prediction (45 min)**

- Posterior predictive checks
- Forecasting with uncertainty
- Comparing to true parameters
- Discussion: Model limitations

**Wrap-up (10 min)**

- Key takeaways
- Extensions and further learning
- Q&A

### Teaching Tips

1. **Run code live**: Don't just show results, run code with students
2. **Encourage experimentation**: Have students modify priors, data, etc.
3. **Use the errors**: If something breaks, use it as a teaching moment
4. **Compare samplers**: Show how different algorithms perform differently
5. **Connect to research**: Ask students about their own research questions

### Common Student Questions

**Q: "How do I choose priors?"**
A: Start with weakly informative priors based on domain knowledge. Show sensitivity analysis by changing priors and re-running.

**Q: "How many iterations do I need?"**
A: Enough for Rhat < 1.1 and ESS > 400. Show them the diagnostics!

**Q: "Why is my model slow?"**
A: For BayesianTools, it's the ODE solving. For Stan, compilation + sampling. Discuss trade-offs.

**Q: "Can I use this for my own data?"**
A: Yes! Show them how to modify the data loading section.

**Q: "Which sampler should I use?"**
A: DEzs is a good default. Show comparison plot from vignette.

**Q: "BayesianTools vs Stan - which for my thesis?"**
A: See COMPARISON.md. Generally: prototype in BayesianTools, final analysis in Stan if needed.

### Issue: MCMC chains haven't converged

**Solution**:

- Increase iterations
- Try different sampler (DEzs usually better than Metropolis)
- Check for coding errors in likelihood
- Use as teaching moment about convergence!

### Issue: Student R environment conflicts

**Solution**:

- Have them restart R session
- Check for package version conflicts
- As last resort: fresh R installation

## After the Course

### Homework Ideas

1. **Change the model**:

   - Add vaccination compartment (SIRV)
   - Model two populations with migration
   - Add births/deaths
2. **Different priors**:

   - Use uniform priors
   - Use informative priors
   - Compare posterior distributions
3. **Real data**:

   - Find COVID-19 or flu data
   - Fit SIR model
   - Evaluate fit quality
4. **Model comparison**:

   - Fit SEIR instead of SIR
   - Use DIC or WAIC for comparison
   - Discuss which is better

### Further Learning Resources

**Books:**

- Gelman et al. "Bayesian Data Analysis" (the bible)
- McElreath "Statistical Rethinking" (accessible)
- Kruschke "Doing Bayesian Data Analysis" (very accessible)

**Online:**

- Stan documentation and case studies
- BayesianTools package vignettes
- Michael Betancourt's Stan tutorials
- YouTube: Richard McElreath's lectures

**Practice:**

- Stan forums: discourse.mc-stan.org
- Cross Validated (Stack Exchange)
- Kaggle datasets for practice

### Project Ideas

- Apply to student's own research area
- Extend SIR model in meaningful way
- Compare multiple epidemic models
- Hierarchical model with multiple populations

## Technical Notes

### Package Dependencies

**Core:**

- BayesianTools: MCMC sampling
- deSolve: ODE solving
- ggplot2: Visualization

**Optional:**

- rstan: Alternative Bayesian engine
- bayesplot: Enhanced diagnostics
- coda: MCMC diagnostics
