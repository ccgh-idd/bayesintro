# Stan vs. BayesianTools: Which Should I Choose?

This document helps you decide which vignette to start with for learning Bayesian inference with SIR models.

## Quick Recommendation

**Start with BayesianTools if this is your first time with Bayesian inference.** It's pure R, requires no compilation, and helps you understand the fundamentals. Once comfortable, explore Stan for more complex projects.

## Detailed Comparison

| Feature                       | BayesianTools                       | Stan                         |
| ----------------------------- | ----------------------------------- | ---------------------------- |
| **Installation**        | Simple (`install.packages()`)     | Requires C++ compiler setup  |
| **Learning Curve**      | Gentle - pure R code                | Steeper - new language       |
| **Compilation**         | None needed ✓                      | ~1 minute per model          |
| **Speed (SIR model)**   | ~5 mins for 3 samplers              | ~3 mins with HMC             |
| **Code Transparency**   | Full R code you can modify          | Stan code + R wrapper        |
| **Understanding MCMC**  | Excellent - see algorithms clearly  | More "black box"             |
| **Sampler Options**     | DEzs, DREAM, Metropolis, AM, + more | HMC (state-of-the-art)       |
| **Diagnostics**         | Good built-in tools                 | Excellent (via bayesplot)    |
| **Scalability**         | Good for simple-moderate models     | Excellent for complex models |
| **Industry Use**        | Academic/teaching                   | Production/research standard |
| **Error Messages**      | R errors (familiar)                 | C++ errors (can be cryptic)  |
| **Model Flexibility**   | Moderate                            | Very high                    |
| **Hierarchical Models** | Possible but manual                 | Natural syntax               |
| **Parallel Chains**     | Yes                                 | Yes (better optimized)       |
| **Documentation**       | Good package docs                   | Extensive (book, forums)     |

## Pedagogical Advantages

### BayesianTools is Better for Teaching:

1. **Transparency**: Students see the entire likelihood function in R
2. **Experimentation**: Easy to modify priors, likelihood, and compare
3. **Algorithm Understanding**: Can try different MCMC methods and see differences
4. **No Technical Barriers**: Works on any computer with R
5. **Immediate Feedback**: No compilation wait time
6. **Debugging**: Standard R debugging tools work

### Stan is Better for Advanced Learning:

1. **Professional Skills**: Stan is industry standard
2. **Efficiency**: HMC is very efficient for complex models
3. **Automatic Differentiation**: No need to calculate gradients manually
4. **Scalability**: Built for large, complex hierarchical models
5. **Community**: Large user base and extensive resources
6. **Best Practices**: Enforces good model structure

## Use Cases

### Use BayesianTools When:

- ✅ Teaching Bayesian fundamentals to beginners
- ✅ Exploring different MCMC algorithms
- ✅ Prototyping simple to moderate models
- ✅ You need pure R implementation
- ✅ Installation complexity is a barrier
- ✅ You want to understand MCMC "under the hood"

### Use Stan When:

- ✅ Building production-ready models
- ✅ Working with complex hierarchical structures
- ✅ Need maximum computational efficiency
- ✅ Have many parameters (>20)
- ✅ Using non-conjugate priors with complex posteriors
- ✅ Want to leverage advanced HMC features
- ✅ Need the best automatic tuning
