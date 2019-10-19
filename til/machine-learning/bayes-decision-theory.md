# Bayes Decision Theory

#### The theory how to make a decision under uncertainty.

## Frequentism vs Bayesianism

* Frequentism: probabilities are related to frequency of the events.
  * Criticism: if the prior is wrong, the result will be worse.
* Bayesianism: probabilities are related to our knowledge about the events.
  * generally to get better uncertainty estimates for many situations.

## Basic concepts of bayes decision theory

### 1. Priors: a priori probabilities

$$
p(C_k)
$$

$$
\sum_kp(C_k)=1
$$

* Before seeing the data - by previous experiments or history ➡ **Expectation**

### 2. \(Class-\)Conditional probabilities; Likelihood

$$
p(x|C_k)
$$

* $$x$$ 's likelihood for class $$C_k$$ 
* $$x$$ : a **feature** vector
* $$x$$ measures/describes **certain properties** of the input.

### 3. Posterior probabilities

The probability of class $$C_k$$ given the measurement vector $$x$$.

$$
p(C_k | x) = \frac {p(x|C_k)p(C_k)}{p(x)} = \frac {p(x|C_k)p(C_k)}{\sum_i p(x|C_i)p(C_i)}
$$

$$
Posterior = \frac {Likelihood \times Prior}{Normalization Factor}
$$

* Normalize each point so that the sum of the all possible outcome is **1**.
* Based on this, we can find '**Decision boundary**'.
* Posterior gives us the information what class actually more probable is under given measurement\(=$$x$$\).

## Goal of Bayesian Decision Theory

⭐ **Minimize the probability of a misclassification**.

### Misclassification

$$
\begin{align}
p(mistake) &= p(x \in R_1, C_2) + p(x \in R_2, C_1) \\ &= \int_{R_1}p(x, C_2)dx + \int_{R_2}p(x, C_1)dx \\ &= \int_{R_1}p(C_2|x)p(x)dx + \int_{R_2}p(C_1|x)p(x)dx
\end{align}
$$

* Optimal decision - decide the class that has **higher posterior probability;** it minimizes the risk of misclassification.

### Optimal decision Rule

Defice for $$C_1$$:

$$
p(C_1|x) > p(C_2|x)
\Leftrightarrow p(x|C_1)p(C_1) > p(x|C_2)p(C_2)
$$

#### Likelihood-Ratio Test

$$
\frac {p(x|C_1)}{p(x|C_2)} > \frac {p(C_2)}{p(C_1)}
$$

* Same effect with $$p(C_1|x) > p(C_2|x)$$ 
* Ratio of priors: decision threshold $$\theta$$ 

### Classifying with Loss Functions

Generalization to decisions with a **loss function**.

* Differentiate btw. the **possible decisions** and the **possible true** classes
* The cost of loss may be asymmetric
* Formulizing: loss matrix $$L_{kj}$$ 

$$
L_{kj} = \text{loss for decision } C_j \text{ if truth is }C_k
$$

* Different loss functions may lead to different Bayes optimal strategies\(behaviours\) \(e.g. from different actors\).

Optimal solution ➡ one that minimizes the \(the expected\) loss.

* why "the expected loss"?
  * loss function depends on the **true** class, which is **unknown**.

⭐**Solution**⭐   
: The class that higher posterior probability + The decision with minimized expected loss.

### The Reject Option

Classification errors - from the \(reject\) regions where the largest posterior probability btw. two classes is significanly less than 1.

* Relatively uncertain about the class membership.
* e.g. look for another test to show evidence.

### Discriminant Functions

Formulate classification in terms of **comparisons**

$$
y_1(x), ... , y_k(x)\\
y_k(x) = p(C_k|x)
$$

* Generative methods: $$y_k(x) \propto p(x|C_k)p(C_k)$$ 
  * modelling each distribution \(shape\)
  * determin calss membership.
* Discriminative methods: $$y_k(x) = p(C_k|x)$$ 
  * solve th inference problem of determining the posterior class probabilities
  * assign each new $$x$$ to its class.
* Alternative
  * directly find a suitable $$y_k(x)$$ 
  * maps each input $$x$$ directly into a class label 

