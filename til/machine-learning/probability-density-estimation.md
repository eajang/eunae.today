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

   2. Likelihood of **all** data points: $$L(\theta) = p(X|\theta) = \prod_{n=1}^{N}p(x_n|\theta)$$  + taking log \(to simplify\) $$E(\theta) = - \ln L(\theta) = -\sum_{n=1}^{N}\ln p(x_n|\theta)$$ 

   ➡ Maximize the likelihood ~ Minimize the negative log-likelihood

   * True parameter vector $$\theta$$ : unknown, but **fixed**
   * Minimaze a log-likelihood function

     * Take the derivative and set it to zero.

     we can obtain

     *  $$\hat \mu = \frac{1}{N}\sum_{n=1}^{N}x_n \quad \quad\quad \quad \cdots \quad \text{sample mean}$$ 
     * $$\hat \sigma^2 = \frac{1}{N}\sum_{n=1}^{N}(x_n-\hat\mu)^2 \quad \cdots \quad \text{sample variance}$$

   * **Maximum Likelihood estimate for the parameters** of a  Gaussian distribution: $$\hat\theta = (\hat \mu, \hat \sigma)$$ 
   * Limitation
     * **Underestimates** the variance of the distribution
       * Correction: $$\tilde \sigma^2 = \frac{1}{N}\sum_{n=1}^{N}(x_n-\hat\mu)^2 $$
     * Maximum likelihood overfits to the observed data.
   * Maximum Likelihood - Fequentist concept

2. **Bayesian Approach**

   * True parameter vector $$\theta$$: **random** variable
     * Use prior
     * Training data: converts **prior** distribution on $$\theta$$ into a **posterior** probability density.

 

## Method \#2 - Non-parametric representations

The functional form of the distribution is **unknown**.  
➡Estimate probability density from **data** 

#### 1.Histograms

* Partition the data space into distinct **bins**
* $$\Delta_i$$ ****: widths - a smoothing factor
* $$n_i$$ : number of observations in each bin

$$
p_i = \frac{n_i}{N\Delta_i}
$$

* use for any dimensionality
* no need to store data points
* **Problem**
  * consideration about size of **bin**
  * the **required number of bins** grows **exponentially** with dimension --&gt; large number - large number of data points  ➡ good for **low** dimensional data

#### 

#### ✔ Statistically Better-Founded Approach

* Data point $$\mathrm{x}$$ from $$p(\mathrm{x})$$
* Region $$\mathcal{R}$$ 
* Probability that x falls into small region$$\mathcal{R}$$:

$$
P = \int_{\mathcal{R}}p(y)dy
$$

* $$\mathcal{R}$$ sufiiciently small ➡$$p(\mathrm{x})$$ is rouphly constant
  * $$V$$: the volume of $$\mathcal{R}$$

$$
P = \int_{\mathcal{R}}p(y)dy \approx p(\mathrm{x})V
$$

* $$N$$\(the number of samples\) sufficiently large:
  * K: the number of counted samples

$$
P = \frac{K}{N} \Rightarrow p(\mathrm{x}) \approx \frac{K}{NV}
$$

* $$V$$fixed + $$K$$determine\(count\) ➡ **Kernel Methods**
* $$V$$determine + $$K$$fixed ➡**K-Nearest Neibor** 

#### 2. Kernel density estimation

Any kernel with $$k(\mathbf{u}) \geqslant 0$$ and the volumn $$\int k(\mathbf{u})d\mathbf{u} = 1$$ can be used. 

* $$a = b$$: center
* $$\mathrm{x}_n$$: location of each data points

$$
K = \sum_{n=1}^{N}k(\mathrm{x}-\mathrm{x}_n)
$$

$$
p(\mathrm{x}) \approx \frac {K}{NV} = \frac{1}{N}\sum_{n=1}^{N}k(\mathrm{x}-\mathrm{x}_n)
$$

   ****1. **Parzen Window**; a simple kernel function

* Hypercube
  * dimension $$D$$ 
  * edge length $$h$$
* Kernel function 

$$
k(\mathbf{u}) = \begin{cases}
  1,  &|u_i| \le \frac{1}{2}h, \quad i = 1,\dots,D\\
  0, & \text{else}
\end{cases}
$$

$$
V = \int k(\mathbf{u})d\mathbf{u} = h^D
$$

$$
p(\mathrm{x}) \approx \frac {K}{NV} = \frac{1}{Nh^D}\sum_{n=1}^{N}k(\mathrm{x}-\mathrm{x}_n)
$$

* Interpretations of parzen window
  1. Kernel window $$k$$ at location $$\mathrm{x}$$ + count data points which fall inside of kernel window
  2. Kernel window $$k$$ around each data point $$\mathrm{x}_n$$ + sum up their influences\(**overlapped** area\) at location $$\mathrm{x}$$. ➡ visualization of density
* Problem: artificial **discontinuities** at the cube boundaries  ➡ choose a **smoother** kernel profile function \(e.g. Gaussian\)

   2. **Gaussian Kernel**

* Kernel function

$$
k(\mathbf{u}) = \frac {1}{(2\pi h^2)^{1/2}}\exp\biggl\{-\frac {\mathbf{u}^2}{2h^2}\biggr\}
$$

* Volumn is 1 because of the Normalization of Gaussian.

$$
V = \int k(\mathbf{u})d\mathbf{u} =1
$$

$$
p(\mathrm{x}) \approx \frac {K}{NV} = \frac{1}{N}\sum_{n=1}^{N}\frac {1}{(2\pi)^{D/2}h}\exp\biggl\{-\frac {||\mathrm{x} - \mathrm{x}||^2}{2h^2}\biggr\}
$$

* $$h$$: acts as a smoother

#### 3. k-Nearest-Neighbor

## Mixture models

