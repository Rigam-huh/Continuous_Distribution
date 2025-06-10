# Continuous_Distribution
## Continuous Distributions in R: Theory and Implementation

A comprehensive guide to generating and transforming continuous probability distributions in R, covering mathematical foundations and practical implementations.

---

### TABLE OF CONTENTS:
1. Key Features
2. Distributions Covered
3. Mathematical Foundations
4. Installation & Usage
5. Applications
6. License
7. Contact

---

### KEY FEATURES:
- Step-by-step generation of continuous distributions from Uniform(0,1)
- Mathematical proofs for distribution transformations
- R implementations with visualization:
  * Histograms with theoretical density overlays
  * Q-Q plots for distribution validation
- Parameter conversion methods between distributions
- Statistical tests for distribution verification (KS test)

---

### DISTRIBUTIONS COVERED:

1. UNIFORM DISTRIBUTION
   - Base for all transformations
   - R code:
     U <- runif(n, min=0, max=1)

2. EXPONENTIAL DISTRIBUTION
   - Generated via inverse transform:
     Y = -(1/λ)ln(1-U)
   - R code:
     y <- -(1/lambda)*log(1-runif(n))

3. GAMMA DISTRIBUTION
   - Sum of exponential variables
   - Two generation methods:
     a) Sum of exponentials
     b) Built-in rgamma()
   - R code:
     y_gamma <- rowSums(matrix(rexp(n*k, rate=λ), ncol=k))

4. BETA DISTRIBUTION
   - Generated from gamma variables:
     B = X/(X+Y) where X,Y ~ Gamma
   - R code:
     B <- rgamma(n,α,λ)/(rgamma(n,α,λ)+rgamma(n,β,λ))

5. NORMAL DISTRIBUTION
   - Via inverse CDF method:
     Z = Φ⁻¹(U)
   - R code:
     normal_data <- qnorm(runif(n))

6. CHI-SQUARED DISTRIBUTION
   - Sum of squared normals
   - R code:
     chi_sq <- rnorm(n)^2 + rnorm(n)^2 + ...

---

### MATHEMATICAL FOUNDATIONS:
1. Probability Integral Transform:
   If U ~ Uniform(0,1), then F⁻¹(U) ~ F

2. Key Transformations:
   - Exponential: F⁻¹(u) = -ln(1-u)/λ
   - Normal: F⁻¹(u) = Φ⁻¹(u)
   - Gamma: Sum of iid exponentials
   - Beta: Ratio of gammas B = X/(X+Y)

3. Distribution Relationships:
   - χ²ₖ = Gamma(k/2, 1/2)
   - N(0,1)² = χ²₁
   - ΣExp(λ) = Gamma(n, λ)

---

### Example workflow:
# Generate exponential from uniform
lambda <- 3
u <- runif(10000)
exp_samples <- -(1/lambda)*log(1-u)

#### Visualize
hist(exp_samples, prob=TRUE)
curve(dexp(x,lambda), add=TRUE, col="red")

---

# APPLICATIONS:
- Risk modeling (exponential for wait times)
- Statistical inference (normal, chi-squared)
- Bayesian analysis (beta distributions)
- Reliability engineering (gamma distributions)

