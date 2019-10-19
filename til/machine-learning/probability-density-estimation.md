# Probability Density Estimation

#### Estimate\(=learn\) probabilities from data.

* Supervised training case: data, class labels
* Estimate the probability density for each class $$C_k$$ separately from data\(measurement\) $$x_1, x_2, ...$$ .
  * Notation: $$p(x) := p(x|C_k)$$ 

## Method \#1 - Parametric representations

### The Gaussian \(or Normal\) Distribution

One-dimensional case \(2 Parameters\)

* Bell-shape
* Sum of the area under the curve = 1
* Mean $$\mu$$\(center of the curve\)
* Variance $$\sigma^2$$\(wideness of the curve\)

$$
N(x|\mu, \sigma^2) = \frac {1}{\sqrt{2\pi}\sigma}\exp\biggl\{-\frac {(x-\mu)^2}{2\sigma^2}\biggr\}
$$

Multi-dimensional case \(Vector\)

* Mean $$\mu$$, Covariance matrix $$\Sigma$$ 
* Normalization terms

$$
N(\mathrm{x}|\mu, \Sigma) = \frac {1}{(2\pi)^{D/2}|\Sigma|^{1/2}}\exp\biggl\{-\frac {1}{2}(\mathrm{x}-\mu)^T\Sigma^{-1}(\mathrm{x}-\mu)\biggr\}
$$

#### 1. Properties - '**Central Limit Theorem**'

* N independent identically distributed random variables
* The distrubutino of the sum of N i.i.d. random variables - increasingy Gaussian as N grows.

#### 2. Properties - 'Shape of the Gaussian'

* Mahalanobis distance

$$
\Delta^2 = (\mathrm{x} - \mu)^T\Sigma^{-1}(\mathrm{x}-\mu)
$$

* [https://darkpgmr.tistory.com/41](https://darkpgmr.tistory.com/41)
* shape of the Gaussian
  * $$\Sigma$$ : real, symmetric
  * Decompose it into its eigenvalues and eigenvectors  ➡**Constant density on ellipsoids** with main directions along the eigenvectors and scaling factors.
  * Special cases
    * Full covariance matrix ➡ General ellipsoid
    * Diagonal covariant matrix ➡ Axis-aligned ellipsoid
    * Uniform variance ➡ Hypersphere
* The marginals of a Gaussian are again Gaussians

### Parametic Methods

* Different interpretation of data by parameters
* What is the best distribution?
* How do we define it?

➡ Estimation of the parameter $$\theta$$ 

1. Likelihood of $$\theta$$ - **Maximum Likelihood Approach**

   1. Likelihood of **single** data point:

       $$p(x_n|\theta)=\frac {1}{\sqrt{2\pi}\sigma}\exp\{-\frac{(x-\mu)^2}{2\sigma^2}\}$$

   2. Likelihood of **all** data points: $$L(\theta) = p(X|\theta) = \prod_{n=1}^{N}p(x_n|\theta)$$  + taking log \(to simplify\) $$E(\theta) = - \ln L(\theta) = -\Sigma_{n=1}^{N}\ln p(x_n|\theta)$$ 

   ➡ Maximize the likelihood ~ Minimize the negative log-likelihood

   * True parameter vector $$\theta$$ : unknown, but **fixed**
   * Minimaze a log-likelihood function

     * Take the derivative and set it to zero.

     we can obtain

     *  $$\hat \mu = \frac{1}{N}\Sigma_{n=1}^{N}x_n \quad \quad\quad \quad \cdots \quad \text{sample mean}$$ 
     * $$\hat \sigma^2 = \frac{1}{N}\Sigma_{n=1}^{N}(x_n-\hat\mu)^2 \quad \cdots \quad \text{sample variance}$$

   * **Maximum Likelihood estimate for the parameters** of a  Gaussian distribution: $$\hat\theta = (\hat \mu, \hat \sigma)$$ 
   * Limitation
     * **Underestimates** the variance of the distribution
       * Correction: $$\tilde \sigma^2 = \frac{1}{N}\Sigma_{n=1}^{N}(x_n-\hat\mu)^2 $$
     * Maximum likelihood overfits to the observed data.
   * Maximum Likelihood - Fequentist concept

2. **Bayesian Approach**

   * True parameter vector $$\theta$$: **random** variable
     * Use prior
     * Training data: converts **prior** distribution on $$\theta$$ into a **posterior** probability density.

 

## Method \#2 - Non-parametric representations

## Mixture models

