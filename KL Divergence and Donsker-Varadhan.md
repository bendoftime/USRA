Here is the rigorous explanation of the Kullback-Leibler divergence and the Donsker-Varadhan representation, followed by how they are applied in the proof of Theorem 3.2.

### 1. Kullback-Leibler (KL) Divergence

The Kullback-Leibler divergence is a fundamental measure in information theory and statistics that quantifies how one probability distribution differs from a reference probability distribution.

**Definition:** 
Let $P$ and $Q$ be two probability measures on a measurable space $(\mathcal{X}, \mathcal{F})$. Assume $P$ is absolutely continuous with respect to $Q$ (denoted as $P \ll Q$), meaning that for any measurable set $A$, if $Q(A) = 0$, then $P(A) = 0$. By the Radon-Nikodym theorem, there exists a density function (or likelihood ratio) $\frac{dP}{dQ}$ such that $P(A) = \int_A \frac{dP}{dQ} dQ$.

The KL divergence from $Q$ to $P$ is defined as:
$$D_{\text{KL}}(P \| Q) = \mathbb{E}_P \left[ \log \frac{dP}{dQ} \right] = \int_{\mathcal{X}} \log \left( \frac{dP}{dQ} \right) dP$$

If $P$ is not absolutely continuous with respect to $Q$, then $D_{\text{KL}}(P \| Q) = \infty$. 

**Key Property:** 
By expectation Jensen's inequality, $D_{\text{KL}}(P \| Q) \ge 0$, and $D_{\text{KL}}(P \| Q) = 0$ if and only if $P = Q$ almost everywhere. It is not a true metric because it is not symmetric ($D_{\text{KL}}(P \| Q) \neq D_{\text{KL}}(Q \| P)$) and does not satisfy the triangle inequality.

### 2. The Donsker-Varadhan Representation

The Donsker-Varadhan representation is a variational formula that expresses the KL divergence as a supremum over a class of functions. 

**Theorem:**
For any two probability measures $P$ and $Q$ on $\mathcal{X}$,
$$D_{\text{KL}}(P \| Q) = \sup_{f} \left( \mathbb{E}_P[f] - \log \mathbb{E}_Q[e^f] \right)$$
where the supremum is taken over all bounded measurable functions $f: \mathcal{X} \to \mathbb{R}$ (or any measurable function such that the expectations are well-defined).

**Proof:**
We must prove two things: (1) that $\mathbb{E}_P[f] - \log \mathbb{E}_Q[e^f] \le D_{\text{KL}}(P \| Q)$ for all $f$, and (2) that the equality is achieved for a specific choice of $f$.

**Step 1: Upper Bound (Weak Duality)**
Assume $D_{\text{KL}}(P \| Q) < \infty$, which implies $P \ll Q$. Let $p = \frac{dP}{dQ}$ be the Radon-Nikodym derivative. 
Consider the quantity $\mathbb{E}_P[f] - D_{\text{KL}}(P \| Q)$. We can write this as a single integral with respect to $P$:
$$\mathbb{E}_P[f] - D_{\text{KL}}(P \| Q) = \int_{\mathcal{X}} f dP - \int_{\mathcal{X}} \log(p) dP = \int_{\mathcal{X}} \log(e^f) dP - \int_{\mathcal{X}} \log(p) dP = \int_{\mathcal{X}} \log\left(\frac{e^f}{p}\right) dP$$

Since the logarithm function is strictly concave, we can apply Jensen's inequality ($\mathbb{E}[\log(Z)] \le \log(\mathbb{E}[Z])$):
$$\int_{\mathcal{X}} \log\left(\frac{e^f}{p}\right) dP \le \log \left( \int_{\mathcal{X}} \frac{e^f}{p} dP \right)$$

By the definition of the Radon-Nikodym derivative, $dP = p dQ$. Substituting this into the right side:
$$\log \left( \int_{\mathcal{X}} \frac{e^f}{p} p dQ \right) = \log \left( \int_{\mathcal{X}} e^f dQ \right) = \log \mathbb{E}_Q[e^f]$$

We have established:
$$\mathbb{E}_P[f] - D_{\text{KL}}(P \| Q) \le \log \mathbb{E}_Q[e^f]$$
Rearranging the terms yields:
$$\mathbb{E}_P[f] - \log \mathbb{E}_Q[e^f] \le D_{\text{KL}}(P \| Q)$$

**Step 2: Achieving the Supremum**
To show that the supremum equals $D_{\text{KL}}(P \| Q)$, we identify the function $f^*$ that satisfies the equality condition for Jensen's inequality. Jensen's inequality $\mathbb{E}[\log(Z)] \le \log(\mathbb{E}[Z])$ holds with equality if and only if $Z$ is a constant almost surely.

In our proof, the random variable is $Z = \frac{e^f}{p}$. Setting this to a constant (let's choose 1) gives:
$$\frac{e^{f^*}}{p} = 1 \implies e^{f^*} = p \implies f^* = \log p = \log \left( \frac{dP}{dQ} \right)$$

Substitute this optimal function $f^*$ back into the objective:
$$\mathbb{E}_P[f^*] - \log \mathbb{E}_Q[e^{f^*}] = \int_{\mathcal{X}} \log(p) dP - \log \left( \int_{\mathcal{X}} p dQ \right)$$
Since $p dQ = dP$ and $P$ is a probability measure, $\int_{\mathcal{X}} p dQ = \int_{\mathcal{X}} dP = 1$. Therefore, $\log(1) = 0$, and the expression evaluates exactly to:
$$\int_{\mathcal{X}} \log(p) dP - 0 = D_{\text{KL}}(P \| Q)$$
Thus, the supremum is obtained, completing the proof.

### 3. Application to Theorem 3.2

In the proof of Theorem 3.2 (page 19, Equation 21), the authors are minimizing the following objective with respect to the score function $h$:
$$\min_h \left( \mathbb{E}_0[h(Y)] + \log \mathbb{E}_{1, \boldsymbol{P}} [e^{-h(Y)}] \right)$$
where $\mathbb{E}_0$ denotes the expectation under the null distribution $\mu_0$, and $\mathbb{E}_{1, \boldsymbol{P}}$ denotes the expectation under the alternative distribution $\mu_{1, \boldsymbol{P}}$.

To apply the Donsker-Varadhan representation, use the substitution $f = -h$. The minimization problem over $h$ becomes a maximization problem over $f$:
$$\min_h \left( \mathbb{E}_0[h(Y)] + \log \mathbb{E}_{1, \boldsymbol{P}} [e^{-h(Y)}] \right) = \min_f \left( \mathbb{E}_0[-f(Y)] + \log \mathbb{E}_{1, \boldsymbol{P}} [e^{f(Y)}] \right)$$
$$= -\max_f \left( \mathbb{E}_0[f(Y)] - \log \mathbb{E}_{1, \boldsymbol{P}} [e^{f(Y)}] \right)$$

By the Donsker-Varadhan representation (with $P = \mu_0$ and $Q = \mu_{1, \boldsymbol{P}}$), the term inside the maximum is exactly the definition of the KL divergence:
$$-\max_f \left( \mathbb{E}_{\mu_0}[f] - \log \mathbb{E}_{\mu_{1, \boldsymbol{P}}} [e^f] \right) = -D_{\text{KL}}(\mu_0 \| \mu_{1, \boldsymbol{P}})$$

This proves the equality in Equation (21) of the text. 

Furthermore, as derived in Step 2 above, the optimal function $f^*$ that achieves this equality is the log-likelihood ratio $f^* = \log\left(\frac{d\mu_0}{d\mu_{1, \boldsymbol{P}}}\right)$. Since $h = -f$, the optimal score function $h^*$ is:
$$h^* = - \log\left(\frac{d\mu_0}{d\mu_{1, \boldsymbol{P}}}\right) = \log\left(\frac{d\mu_{1, \boldsymbol{P}}}{d\mu_0}\right)$$
This aligns precisely with the paper's definition of the optimal score function $h^\star_{\text{gum}, \Delta}(r)$ stated right below equation (21).





Here is the rigorous proof of why $D_{\text{KL}}(P \| Q) \ge 0$ and why equality holds if and only if $P = Q$. 

This result relies directly on Jensen's inequality.

### 1. Statement of Jensen's Inequality
Let $X$ be an integrable random variable defined on a probability space, and let $\phi$ be a convex function. Jensen's inequality states that:
$$\mathbb{E}[\phi(X)] \ge \phi(\mathbb{E}[X])$$
Furthermore, if $\phi$ is a **strictly convex** function, the equality $\mathbb{E}[\phi(X)] = \phi(\mathbb{E}[X])$ holds if and only if $X$ is a constant almost surely (i.e., $X = c$ with probability 1, for some constant $c$).

### 2. Proof that $D_{\text{KL}}(P \| Q) \ge 0$
By definition, the KL divergence is the expected value of the log-likelihood ratio under the distribution $P$:
$$D_{\text{KL}}(P \| Q) = \mathbb{E}_P \left[ \log \frac{dP}{dQ} \right]$$

To apply Jensen's inequality, we rewrite the term inside the expectation by pulling out a negative sign and taking the reciprocal of the ratio:
$$D_{\text{KL}}(P \| Q) = \mathbb{E}_P \left[ -\log \frac{dQ}{dP} \right]$$

Now, let our random variable be $X = \frac{dQ}{dP}$, and our function be $\phi(t) = -\log(t)$. 
The second derivative of $\phi(t)$ is $\phi''(t) = \frac{1}{t^2} > 0$ for all $t > 0$. Because the second derivative is strictly positive, the function $\phi(t) = -\log(t)$ is strictly convex.

Applying Jensen's inequality to this expectation yields:
$$\mathbb{E}_P \left[ -\log \left(\frac{dQ}{dP}\right) \right] \ge -\log \left( \mathbb{E}_P \left[ \frac{dQ}{dP} \right] \right)$$

Next, we evaluate the expectation on the right side. The expectation of $\frac{dQ}{dP}$ under the distribution $P$ is exactly the integral of $dQ$ over the support of $P$:
$$\mathbb{E}_P \left[ \frac{dQ}{dP} \right] = \int_{\mathcal{X}} \frac{dQ}{dP} dP = \int_{\mathcal{X}} dQ = 1$$
*(Note: $\int dQ = 1$ because $Q$ is a valid probability measure).*

Substitute this back into the right side of the inequality:
$$-\log(1) = 0$$

Therefore, we conclude:
$$D_{\text{KL}}(P \| Q) \ge 0$$

### 3. Proof of the Equality Condition ($D_{\text{KL}} = 0 \iff P = Q$)

Because the function $\phi(t) = -\log(t)$ is **strictly** convex, the equality in Jensen's inequality holds if and only if the random variable $X = \frac{dQ}{dP}$ is a constant almost everywhere with respect to $P$. https://www.math.mcgill.ca/dstephens/556-2014/Handouts/Math556-05-Inequalities.pdf

**Direction 1: If $D_{\text{KL}}(P \| Q) = 0$, then $P = Q$**
If the divergence is exactly zero, the equality condition of Jensen's inequality must be met. This means:
$$\frac{dQ}{dP} = c \quad (P\text{-almost everywhere})$$
for some constant $c$. 

We already established that $\mathbb{E}_P \left[ \frac{dQ}{dP} \right] = 1$. Substituting $c$ into this expectation gives:
$$\mathbb{E}_P[c] = 1 \implies c = 1$$

Thus, $\frac{dQ}{dP} = 1$ almost everywhere. This immediately implies that $dP = dQ$ almost everywhere, meaning the two probability measures are identical: $P = Q$.

**Direction 2: If $P = Q$, then $D_{\text{KL}}(P \| Q) = 0$**
If $P = Q$ almost everywhere, then the Radon-Nikodym derivative $\frac{dP}{dQ} = 1$ almost everywhere. 
Substituting this directly into the definition of KL divergence yields:
$$D_{\text{KL}}(P \| Q) = \mathbb{E}_P \left[ \log(1) \right] = \mathbb{E}_P [0] = 0$$

This completes the proof.