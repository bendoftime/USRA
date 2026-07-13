##### Gumbel-max Watermark

> [!lemma] 
> If $X \sim U(0, 1),$ $Y = -\ln(X)$, then $Y \sim \text{Exp}(1)$

`Proof.`
This is clear by manipulating their CDF.
`QED.`

Now $$\arg\max_{w} \frac{\log U_w}{P_w} \iff \arg\min_{w} \frac{-\log U_w}{P_w} \iff \arg\min_{w} \frac{Exp(1)}{P_w}$$
Note (by property of Exp or Gamma, as we learned in stat 450), 
$$Y_w :=\frac{Exp(1)}{P_w}\sim Exp(\lambda = P_w)$$
By stat 333,

> [!lemma] 
> Let $\{X_i\}_{i=1}^n$ be a sequence of independent rvs where $X_i \sim \text{EXP}(\lambda_i), \ i = 1, 2, \ldots, n$. For $j \in \{1, 2, \ldots, n\}$, $\mathbb{P}(X_j = \min\{X_1, X_2, \ldots, X_n\})=\frac{\lambda_j}{\sum_{i=1}^n \lambda_i}$ 

 `Proof.`
$$\begin{aligned}
    &\mathbb{P}(X_j = \min\{X_1, X_2, \ldots, X_n\})\\ 
    =& \mathbb{P}(X_j < X_1, X_j < X_2, \ldots, X_j < X_n) \\
    =& \int_0^{\infty} \mathbb{P}(X_j < X_1, X_j < X_2, \ldots, X_j < X_n \mid X_j = x) \lambda_j e^{-\lambda_j x} \, dx \\
    =& \int_0^{\infty} \mathbb{P}(X_1 > x, X_2 > x, \ldots, X_n > x) \lambda_j e^{-\lambda_j x} \, dx \quad \text{(since $X_j$ is independent of $\{X_i\}_{i \ne j}$)} \\
    =& \int_0^{\infty} \mathbb{P}(X_1 > x)\mathbb{P}(X_2 > x) \cdots \mathbb{P}(X_n > x) \lambda_j e^{-\lambda_j x} \, dx \\
    =& \int_0^{\infty} e^{-\lambda_1 x} e^{-\lambda_2 x} \cdots e^{-\lambda_n x} \lambda_j e^{-\lambda_j x} \, dx \\
    =& \int_0^{\infty} \lambda_j e^{-(\sum_{i=1}^n \lambda_i) x} \, dx \\
    =& \frac{\lambda_j}{\sum_{i=1}^n \lambda_i} \int_0^{\infty} \left( \sum_{i=1}^n \lambda_i \right) e^{-(\sum_{i=1}^n \lambda_i) x} \, dx \\
    =& \frac{\lambda_j}{\sum_{i=1}^n \lambda_i}
    \end{aligned}$$
`QED.`
Therefore $$\mathbb{P}(Y_w \text{ is the minimum}) = \frac{P_w}{1} = P_w$$
and $\{ \arg\min_{k \in W} Y_k = w \}=\{ Y_{w} \;is \; minimum\}$ as events, so we are done.
















##### Proof of Theorem 2.1

**Consider equation (30):**

- Consider the $1^{st}$ inequality.
Observe 
$$\mathbb{E}_1[T_h(Y_{1:n})] = 1 \cdot \mathbb{P}_1(T_h = 1) + 0 \cdot \mathbb{P}_1(T_h = 0) = \mathbb{P}_1(T_h = 1)$$
And so 
$$1 - \mathbb{E}_1[T_h(Y_{1:n})] = \mathbb{P}_1(T_h = 0)$$
Write 
$$\mathbb{P}_1(T_h = 0) = \mathbb{P}_1\left( \sum_{t=1}^n h(Y_t) < \gamma_{n,\alpha} \right) =\mathbb{P}_1\left( \sum_{t=1}^n -h(Y_t) > -\gamma_{n,\alpha} \right)$$
If $\sum_{i=1}^{n}-h(Y_{t})>-\gamma_{n,\alpha}$, then $\theta\sum_{i=1}^{n}-h(Y_{t})>-\theta\gamma_{n,\alpha}$, thus $$\exp\left( \sum_{i=1}^{n}-\theta h(Y_{t}) \right)> \exp\left( -\theta\gamma_{n,\alpha} \right)$$
By Markov, for nonnegative $Z$, $a>0$, $\mathbb{P}(Z\geq a)\leq \frac{\mathbb{E}[Z]}{a}$, so
$$\mathbb{P}_{1}\left( \sum_{i=1}^{n}-h(Y_{t})>-\gamma_{n,\alpha} \right)\leq \frac{\mathbb{E}_{1}[\exp\left( \sum_{i=1}^{n}-\theta h(Y_{t}) \right)]}{\exp\left( -\theta\gamma_{n,\alpha} \right)}$$
(In discrete case, note $\mathbb{P}(Z > a) \le \mathbb{P}(Z \ge a)$. In cts case, they are equal.)


- Consider the $2^{nd}$ inequality
Since
$$\mathbb{E}_{H_1} \exp\left( \sum_{t=1}^n -\theta h(Y_t) \right) = \mathbb{E}_{H_1} \left[ \prod_{t=1}^n \exp(-\theta h(Y_t)) \right]$$
By tower rule,
$$
\begin{align}
\mathbb{E}_{H_1} \left[ \prod_{t=1}^n \exp(-\theta h(Y_t)) \right]
&=\mathbb{E}_{H_1}\left[\mathbb{E}_{H_1}\left[\prod_{t=1}^n \exp(-\theta h(Y_t))\mid  (w_{1:(t-1)}, \zeta_{1:(t-1)})\right]\right] \\
&= \mathbb{E}_{H_1} \left[ \left( \prod_{t=1}^{n-1} \exp(-\theta h(Y_t)) \right) \mathbb{E}_{H_1} [\exp(-\theta h(Y_n)) \mid (w_{1:(t-1)}, \zeta_{1:(t-1)})] \right]
\end{align}
$$
By **working hypothesis 2.1** (here $P_t$ is known and $\zeta_{t}$ independent), this is 
$$\mathbb{E}_{H_1} \left[ \left( \prod_{t=1}^{n-1} \exp(-\theta h(Y_t)) \right) \mathbb{E}_{1, P_n} [\exp(-\theta h(Y_n))] \right]$$
Note
$$\mathbb{E}_{1, P_n} [\exp(-\theta h(Y_n))]=\exp(\log \phi_{P_{n,h}}(\theta))\leq\exp(\log \phi_{\mathcal{P},h}(\theta))$$
where $\phi_{\mathcal{P}, h}(\theta) = \sup_{P \in \mathcal{P}} \phi_{P, h}(\theta) = \sup_{P \in \mathcal{P}} \mathbb{E}_{1, P} [\exp(-\theta h(Y))]$.

And by repeatedly doing above from $t=n-1$ to $t=1$, $$\mathbb{E}_{H_1} \left[ \prod_{t=1}^n \exp(-\theta h(Y_t)) \right] \le \left( \exp(\log \phi_{\mathcal{P}, h}(\theta)) \right)^n = \exp(n \cdot \log \phi_{\mathcal{P}, h}(\theta))$$
For the last equality in the proof,
$$ \inf_{\theta\ge 0} \exp\Big( \theta \mathbb{E}_0 h(Y) + \log \phi_{\mathcal{P},h}(\theta) \Big) = \exp\left( \inf_{\theta\ge 0} \left[ \theta \mathbb{E}_0 h(Y) + \log \phi_{\mathcal{P},h}(\theta) \right] \right)$$
as $\exp$ is continuous and monotone increasing.


**Intuition for equation (29) and its proof**

To control type 1 error, for $\alpha \in(0,1)$
$$\mathbb{P}_{H_0} \left( \sum_{t=1}^n h(Y_t) \ge \gamma_{n,\alpha} \right) = \alpha$$
which is $$\mathbb{P}_{H_0} \left( \frac{1}{n} \sum_{t=1}^n h(Y_t) \ge \frac{\gamma_{n,\alpha}}{n} \right) = \alpha$$
Under $H_{0}$, $Y_{i}$ are iid. Thus by SLLN, $$\frac{1}{n} \sum_{t=1}^n h(Y_t) \xrightarrow{a.s.} \mathbb{E}_0 h(Y)$$
So we guess $$\lim_{n \to \infty} \frac{\gamma_{n,\alpha}}{n} = \mathbb{E}_0 h(Y)$$
because otherwise, $\alpha$ will go to either 0 or 1.

Using contradiction, the paper shows $$\limsup_{n\to\infty} \frac{\gamma_{n,\alpha}}{n} \le \mathbb{E}_0 h(Y)$$ and $$\liminf_{n\to\infty} \frac{\gamma_{n,\alpha}}{n} \ge \mathbb{E}_0 h(Y)$$
and so the limit exists and equals $\mathbb{E}_0 h(Y)$.
























##### KL Divergence and Donsker-Varadhan

> [!definition] 
> Let $P$ and $Q$ be two probability measures on a measurable space $(\mathcal{X}, \mathcal{F})$. Assume $P$ is absolutely continuous with respect to $Q$ (denoted as $P \ll Q$), meaning that for any measurable set $A$, if $Q(A) = 0$, then $P(A) = 0$. By the Radon-Nikodym theorem, there exists a density function (or likelihood ratio) $\frac{dP}{dQ}$such that $P(A) = \int_A \frac{dP}{dQ} dQ$.
> 
> The KL divergence from $Q$ to $P$ is defined as:
$$D_{\text{KL}}(P \| Q) = \mathbb{E}_P \left[ \log \frac{dP}{dQ} \right] = \int_{\mathcal{X}} \log \left( \frac{dP}{dQ} \right) dP$$
If $P$ is not absolutely continuous with respect to $Q$, then $D_{\text{KL}}(P \| Q) = \infty$. 

> [!remark] 
> Note that every distribution is a probability measure (push forward measure): $F_X(x) = \mathbb{P}\circ X^{-1}((-\infty, x])$. By Carathéodory extension thm, CDF uniquely determines its probability measure.
> 

> [!remark] 
> By expectation Jensen's inequality, where $-\log$ is convex, $D_{\text{KL}}(P \| Q) \ge 0$, and $D_{\text{KL}}(P \| Q) = 0$ if and only if $P = Q$ almost everywhere.
> 


> [!theorem] Jensen's inequality
> Suppose that $X$ is a random variable with expectation $\mu$, and function $g$ is convex and finite. Then $$ \mathbb{E}_X [g(X)] \ge g(\mathbb{E}_X [X]) $$
> with equality if and only if, for every line $a + bx$ that is a tangent to $g$ at $\mu$ $$ \mathrm{P}_X[g(X) = a + bX] = 1. $$
> https://www.math.mcgill.ca/dstephens/556-2014/Handouts/Math556-05-Inequalities.pdf


> [!corollary]
> Suppose $g$ is strictly convex and finite. Then $\mathbb{E}[g(X)] = g(\mathbb{E}[X])$ if and only if $\mathbb{P}[X = \mu] = 1$

`Proof.`
$\implies:$ Assume $\mathbb{E}[g(X)] = g(\mathbb{E}[X])$. By theorem, for any tangent line $L(x) = a + bx$ to $g$ at the point $\mu$, we have $\mathbb{P}[g(X) = a + bX] = 1$. Because $g$ is convex and finite, it possesses at least one subgradient at $\mu$ (This is fact 9.12 and corollary 9.13 in my co463 notes). Therefore, there exists at least one line $L(x) = a + bx$ that is tangent to $g$ at $\mu$. This guarantees the existence of $a$ and $b$ such that $g(\mu) = a + b\mu$. By the definition of strict convexity, a strictly convex function intersects any of its tangent lines at exactly one point: the point of tangency. Therefore, for all $x \neq \mu$, we have a strict inequality: $g(x) > a + bx$. Consequently, the equation $g(x) = a + bx$ holds true if and only if $x = \mu$. Define the events $A = \{\omega \in \Omega \mid g(X(\omega)) = a + bX(\omega)\}$ and $B = \{\omega \in \Omega \mid X(\omega) = \mu\}$. Then $g(X(\omega)) = a + bX(\omega) \iff X(\omega) = \mu$ holds for every $\omega$ by above. That is $A = B$. Recall we know $\mathbb{P}(A) = 1$. So $\mathbb{P}(B) = 1$, which means $\mathbb{P}[X = \mu] = 1$.

$\impliedby:$ Assume $\mathbb{P}[X = \mu] = 1$. Let $L(x) = a + bx$ be an arbitrary tangent line to $g$ at $\mu$. 4. Because $L(x)$ is tangent to $g$ at $\mu$, then $g(\mu) = a + b\mu$. Since $\mathbb{P}[X = \mu] = 1$, then $\mathbb{P}[g(X) = g(\mu)] = 1$, $\mathbb{P}[a + bX = a + b\mu] = 1$. Since $g(\mu) = a + b\mu$, then $\mathbb{P}[g(X) = a + bX] = 1$. This holds for every line $a+bx$ tangent to $g$ at $\mu$. Thus by theorem, $\mathbb{E}[g(X)] = g(\mathbb{E}[X])$.
`QED.`


> [!theorem] The Donsker-Varadhan Representation
> For any two probability measures $P$ and $Q$ on $\mathcal{X}$, $$D_{\text{KL}}(P \| Q) = \sup_{f} \left( \mathbb{E}_P[f] - \log \mathbb{E}_Q[e^f] \right)$$
>  where the supremum is taken over all bounded measurable functions $f: \mathcal{X} \to \mathbb{R}$ (or any measurable function such that the expectations are well-defined).
> 

> [!remark] 
> We say "taken over any measurable function such that the expectations are well-defined" is because, if we only require boundedness (which is the bare minimum if we want the representation to be well defined), the optimal function $f^* = \log\left(\frac{dP}{dQ}\right)+\log c$ below is usually not bounded.
> 


`Proof.`

We prove it by proving 
- $\mathbb{E}_P[f] - \log \mathbb{E}_Q[e^f] \le D_{\text{KL}}(P \| Q)$ for all $f$, 
- the equality is achieved for some specific $f$.

Assume $D_{\text{KL}}(P \| Q) < \infty$, and so $P \ll Q$. Let $p = \frac{dP}{dQ}$ be the Radon-Nikodym derivative. 
Consider the quantity $\mathbb{E}_P[f] - D_{\text{KL}}(P \| Q)$. We can write this as a single integral with respect to $P$: $$\mathbb{E}_P[f] - D_{\text{KL}}(P \| Q) = \int_{\mathcal{X}} f dP - \int_{\mathcal{X}} \log(p) dP = \int_{\mathcal{X}} \log(e^f) dP - \int_{\mathcal{X}} \log(p) dP = \int_{\mathcal{X}} \log\left(\frac{e^f}{p}\right) dP$$
$$\mathbb{E}_P[f] - D_{\text{KL}}(P \| Q) = \int_{\mathcal{X}} f dP - \int_{\mathcal{X}} \log(p) dP = \int_{\mathcal{X}} \log(e^f) dP - \int_{\mathcal{X}} \log(p) dP = \int_{\mathcal{X}} \log\left(\frac{e^f}{p}\right) dP$$
Since log is concave, by Jensen's inequality, ($\mathbb{E}[\log(Z)] \le \log(\mathbb{E}[Z])$): $$\int_{\mathcal{X}} \log\left(\frac{e^f}{p}\right) dP \le \log \left( \int_{\mathcal{X}} \frac{e^f}{p} dP \right)$$
By Radon-Nikodym, $dP = p dQ$,
$$\log \left( \int_{\mathcal{X}} \frac{e^f}{p} p dQ \right) = \log \left( \int_{\mathcal{X}} e^f dQ \right) = \log \mathbb{E}_Q[e^f]$$
Thus
$$\mathbb{E}_P[f] - D_{\text{KL}}(P \| Q) \le \log \mathbb{E}_Q[e^f]$$
Which is
$$\mathbb{E}_P[f] - \log \mathbb{E}_Q[e^f] \le D_{\text{KL}}(P \| Q)$$

It is clear that if the equality in the Jensen's inequality is attained, then we are done. Note that the function $\phi(t) = -\log(t)$ is strictly convex and finite in $t>0$ (log is strictly concave).

By the above corollary, the equality holds iff $Z=\frac{e^{f^{*}}}{p}=c$ almost surely, where $c$ is the mean of $Z$ and $f^{*}$ is our optimal function. Then $$\frac{e^{f^*}}{p} = c \implies e^{f^*} = cp \implies f^* = \log p +\log c = \log \left( \frac{dP}{dQ} \right)+\log c$$
Substitute this optimal function $f^*$ back into the objective: $$
\begin{align}
&\mathbb{E}_P[f^*] - \log \mathbb{E}_Q[e^{f^*}] \\
=& \mathbb{E}_P[\log(p) + \log(c)] - \log \mathbb{E}_Q[e^{\log(p) + \log(c)}] \\
=&\mathbb{E}_P[\log(p)] + \log(c) - \log \left( c \cdot \mathbb{E}_Q[p] \right) \\
=&D_{\text{KL}}(P||Q) + \log(c) - \log(c) - \log(1) \\
=&D_{\text{KL}}(P||Q)
\end{align}$$
where
$$\mathbb{E}_Q[p]=1$$
since $p dQ = dP$ and $P$ is a probability measure, so $\int_{\mathcal{X}} p dQ = \int_{\mathcal{X}} dP = 1$.

Therefore the sup is attained by $f^{*}$.
Note that from the derivation above, such $f^{*}$ is not unqiue, we can take any valid $c$ we want. We usually take $c=1$.
`QED.`







##### Proof of Theorem 3.2, first part

> [!theorem] 
> Let $h^{\star}_{\mathrm{gum},\Delta}:[0,1]\mapsto \mathbb{R}$ be defined as $h^{\star}_{\mathrm{gum}, \Delta}(r) = \log\left( \left\lfloor \frac{1}{1 - \Delta} \right\rfloor r^{\frac{\Delta}{1 - \Delta}} + r^{\frac{\widetilde{\Delta}}{1 - \widetilde{\Delta}}} \right) \quad \textit{with} \quad \widetilde{\Delta} = (1 - \Delta)\left\lfloor \frac{1}{1 - \Delta} \right\rfloor$.
> This function gives the optimal $\mathcal{P}_\Delta$-efficiency rates in the sense that $R_{\mathcal{P}_\Delta}(h^{\star}_{\mathrm{gum},\Delta}) \ge R_{\mathcal{P}_\Delta}(h)$ for any measurable function $h$. Moreover, $R_{\mathcal{P}_\Delta}(h^{\star}_{\mathrm{gum},\Delta})$ is attained at the following least-favorable NTP distribution in $\mathcal{P}_\Delta$: $$\boldsymbol{P}_{\Delta}^{\star} = \left( \underbrace{1 - \Delta, \dots, 1 - \Delta}_{\lfloor \frac{1}{1 - \Delta} \rfloor \text{ times}}, 1 - (1 - \Delta) \cdot \left\lfloor \frac{1}{1 - \Delta} \right\rfloor, 0, \dots \right)$$
> 


The paper proves $R_{P_{\Delta}}\!\left(h^{\star}_{\mathrm{gum},\Delta}\right)\ge R_{P_{\Delta}}(h)$ by doing the following: 

Recall from "optimality via minimax optimization", finding the optimal $h$ that gives $\sup_{h}R_{\mathcal{P}}(h)$ is reduced to solving $\min_{h}\max_{P\in\mathcal{P}} L(h,P)$ where $L(h,P) := \mathbb{E}_0\, h(Y) \;+\; \log \mathbb{E}_{1,P}\, e^{-h(Y)}$.

The paper shows $$\min_{h}\max_{P\in\mathcal{P}} L(h,P)\geq -D_{KL}(\mu_{0},\mu_{1},P_{\Delta}^{\star})$$
But the paper also shows the min is attained at $$\max_{P\in\mathcal{P}_{\Delta}} L\left(h^{\star}_{\mathrm{gum},\Delta}, P\right)=-D_{KL}(\mu_{0},\mu_{1},P_{\Delta}^{\star})$$
And so this $h^{\star}_{\mathrm{gum},\Delta}$ is the (*unique*) score function that solves the minimax problem

The following are the technical details:


We first claim that the radon-nikodym derivative $\frac{\mathrm{d}\mu_{1,\boldsymbol{P}^\star_\Delta}}{\mathrm{d}\mu_0}$ exists, that is, $\mu_{1,\boldsymbol{P}^\star_\Delta} \ll \mu_0$.
`Proof.`
It is clear that $\mu_{0}$, which is $Y_{t}^{gum}$ under $H_{0}$, follows a $U(0,1)$ distribution. Hence $\mu_{0}$ is the Lebesgue measure on $[0,1]$. Thus for any mble set $A$, $\mu_{0}(A)=\int_{A\cap[0,1]}1  \, dr=0$ implies $A\cap[0,1]$ has length 0.

$\mu_{1,\boldsymbol{P}^\star_\Delta}$, which is the distribution of $Y_{t}^{gum}$ under $H_{1}$ at the "least-favorable NTP distribution". By lemma 3.1, we have CDF $$\sum_{w \in \mathcal{W}} P_w r^{1/P_w}$$
for $r\in(0,1)$. It is clear that since $U_{t,w}\sim U(0,1)$, for $r\leq0$ and $r\geq1$, the CDF is 0 and 1 respectively. Thus we see the support of $\mu_{1,\boldsymbol{P}^\star_\Delta}$ is between $[0,1]$.

Now $$\mu_{1,\boldsymbol{P}^\star_\Delta}(A)=\int_{A\cap[0,1]} f_{1}(r) \, dr$$
where $f_{1}(r)$ is the density of $\mu_{1,\boldsymbol{P}^\star_\Delta}$ distribution (we will derive it later).

Therefore, if $\mu_{0}(A)=0$, then $\mu_{1,\boldsymbol{P}^\star_\Delta}(A)=0$, hence $\mu_{1,\boldsymbol{P}^\star_\Delta} \ll \mu_0$.
`QED.`

Thus we can define the radon-nikodym derivative $$\frac{\mathrm{d}\mu_{1,\boldsymbol{P}^\star_\Delta}}{\mathrm{d}\mu_0}$$


**Consider equation 21:**
To apply the Donsker-Varadhan representation (we are allowed to do so because the radon-nikodym derivative exists), use the substitution $f = -h$: $$
\begin{align}
\min_h \left( \mathbb{E}_0[h(Y)] + \log \mathbb{E}_{1, \boldsymbol{P}} [e^{-h(Y)}] \right) &= \min_f \left( \mathbb{E}_0[-f(Y)] + \log \mathbb{E}_{1, \boldsymbol{P}} [e^{f(Y)}] \right) \\
&= -\max_f \left( \mathbb{E}_0[f(Y)] - \log \mathbb{E}_{1, \boldsymbol{P}} [e^{f(Y)}] \right)
\end{align}$$
By the Donsker-Varadhan representation (with $P = \mu_0$ and $Q = \mu_{1, \boldsymbol{P}}$), $$-\max_f \left( \mathbb{E}_{\mu_0}[f] - \log \mathbb{E}_{\mu_{1, \boldsymbol{P}}} [e^f] \right) = -D_{\text{KL}}(\mu_0 \| \mu_{1, \boldsymbol{P}})$$

We know what is this $f$, it is the $f^{*}$ that we derived before! But we do not know what is $\log \left( \frac{dP}{dQ} \right)$.
By definition, $$ \mu_0(A) = \int_A f_0(r) \, \mathrm{d}r $$ $$ \mu_{1,\boldsymbol{P}^\star_\Delta}(A) = \int_A f_1(r) \, \mathrm{d}r $$
where $f_{0}$, $f_{1}$ are the density function of distributions $\mu_{0}$ and $\mu_{1,\boldsymbol{P}^\star_\Delta}$.


**We wish to find $g$ such that** $$\mu_{1,\boldsymbol{P}^\star_\Delta}(A) = \int_A g(r) \, \mathrm{d}\mu_0$$
From definition, it suffices to find $$\mu_{1,\boldsymbol{P}^\star_\Delta}(A) = \int_A g(r) \left( f_0(r) \, \mathrm{d}r \right)$$
Compare with above (because $f_{0}(r)=1\neq0$), $$g(r)=\frac{f_{1}(r)}{f_{0}(r)}$$
Therefore $$\frac{\mathrm{d}\mu_{1,\boldsymbol{P}^\star_\Delta}}{\mathrm{d}\mu_0}=\frac{f_{1}(r)}{f_{0}(r)}$$

**Now back to the proof of theorem 3.2, in equation 21,**

As we have seen in the proof of The Donsker-Varadhan Representation, the specific $h=-f$ that makes the equality hold (which is also our desired minimizer $h$) is (by taking $c=1$, so $\log c=0$) $$h^\star_{\text{gum},\Delta}(r) = \log \frac{\mathrm{d}\mu_{1,\boldsymbol{P}^\star_\Delta}}{\mathrm{d}\mu_0}(r) = \log \left( \frac{f_1(r)}{f_0(r)} \right)$$
Now we need to figure out what that is. It is clear that $f_{0}(r)=1$


**What is $f_{1}(r)$?**

By lemma 3.1, under $H_{1}$, the distribution of $Y_{t}^{gum}$ given $P_{t}$ obeys $$\mathbb{P}_{H_1}(Y_t^{\mathrm{gum}} \le r \mid P_t) = \sum_{w \in \mathcal{W}} P_{t,w} r^{1/P_{t,w}} \quad \text{for } r \in [0, 1]$$
By taking its derivative, we obtain the density: $$\frac{\mathrm{d}}{\mathrm{d}r} \left( \sum_{w \in \mathcal{W}} P_{t,w} r^{1/P_{t,w}} \right) = \sum_{w \in \mathcal{W}} P_w \left( \frac{1}{P_w} r^{\frac{1}{P_w} - 1} \right) = \sum_{w \in \mathcal{W}} r^{\frac{1 - P_w}{P_w}}$$
By subbing in $\boldsymbol{P}^\star_\Delta$, we can get $f_{1}(r)$.

Recall $$
\begin{align}
\boldsymbol{P}_{\Delta}^{\star}
&= \left( \underbrace{1 - \Delta, \cdots, 1 - \Delta}_{\left\lfloor  \frac{1}{1 - \Delta}  \right\rfloor \text{ times}}, 1 - (1 - \Delta) \cdot \left\lfloor \frac{1}{1 - \Delta} \right\rfloor, 0, \cdots \right) \\
&=\left( \underbrace{1 - \Delta, \cdots, 1 - \Delta}_{\left\lfloor  \frac{1}{1 - \Delta}  \right\rfloor \text{ times}}, 1 - \widetilde{\Delta}, 0, \cdots \right)
\end{align}$$
by defining $\widetilde{\Delta} = (1 - \Delta)\left\lfloor \frac{1}{1 - \Delta} \right\rfloor$.

Therefore $$f_{1}(r)=\left\lfloor \frac{1}{1-\Delta} \right\rfloor r^{\frac{\Delta}{1-\Delta}} + r^{\frac{\tilde{\Delta}}{1-\tilde{\Delta}}}$$
and we get the desired $h^{\star}_{\mathrm{gum},\Delta}$, which is non-decreasing in $r$.

And the rest is clear by the paper.
`QED.`













##### Proof of lemma 3.2, 3.3 and lemma 3.4

**lemma 3.2:**

derivative: Use $r^{1/P_i} = e^{\frac{\ln r}{P_i}}$


**lemma 3.3:**

> [!remark] 
> $\mathcal{P}_\Delta$ is compact and convex by definition

`Proof.`
By definition $\mathcal{P}_\Delta := \left\{ \boldsymbol{P} : \max_{w \in \mathcal{W}} P_w \le 1 - \Delta \right\}$, which is $$\mathcal{P}_\Delta = \left\{ \boldsymbol{P} \in \mathbb{R}^{\lvert \mathcal{W} \rvert}  : \sum_{w \in \mathcal{W}} P_w = 1, \quad 0 \le P_w \le 1 - \Delta \quad \text{for all } w \in \mathcal{W} \right\}$$
Verification of convexity is clear.

To prove compactness, since we are in $\mathbb{R}^{n}$, by Heine-Borel, it suffices to prove closed and bounded.

**Closeness:**
- Let $A := \left\{ \boldsymbol{P} \in \mathbb{R}^{\lvert \mathcal{W} \rvert} : \sum_{w \in \mathcal{W}} P_w = 1 \right\}$. The function $f(\boldsymbol{P}) = \sum P_w$ is continuous. The set $A$ is the preimage of the closed singleton set $\{1\}$ under $f$, meaning $A$ is closed.
- For each $w \in \mathcal{W}$, $B_w = \left\{ \boldsymbol{P} \in \mathbb{R}^{\lvert \mathcal{W} \rvert} : P_w \ge 0 \right\}$. The projection function $g_w(\boldsymbol{P}) = P_w$ is continuous. The set $B_w$ is the preimage of the closed interval $[0, \infty)$ under $g_w$, meaning $B_w$ is closed.
- For each $w \in \mathcal{W}$, $C_w = \left\{ \boldsymbol{P} \in \mathbb{R}^{\lvert \mathcal{W} \rvert} : P_w \le 1 - \Delta \right\}$. Using the same continuous projection $g_w(\boldsymbol{P}) = P_w$, $C_w$ is the preimage of the closed interval $(-\infty, 1 - \Delta]$, meaning $C_w$ is closed.
Note $$\mathcal{P}_\Delta = A \cap \left( \bigcap_{w \in \mathcal{W}} B_w \right) \cap \left( \bigcap_{w \in \mathcal{W}} C_w \right)$$
Thus it is closed.

**Boundedness:**
$$\|\boldsymbol{P}\|_2 = \sqrt{\sum_{w \in \mathcal{W}} P_w^2} \le \sqrt{\sum_{w \in \mathcal{W}} 1^2} = \sqrt{\lvert \mathcal{W} \rvert }$$
`QED.`


**lemma 3.4:**

What does it mean by **permutation invariance**: 
$$\phi_h(\boldsymbol{P}) = \int_0^1 e^{-h(r)} dF_{1,P}(r)$$ where $F_{1,P}(r) = \sum_{w=1}^{|\mathcal{W}|} P_w r^{1/P_w}$.




Proof of lemma 3.4:

What does it mean by "It suffices to demonstrate that any point in $\mathcal{P}_\Delta$ is in the convex hull of $\Pi(\boldsymbol{P}_{\Delta}^{\star})$, denoted by $\mathrm{Conv}(\Pi(\boldsymbol{P}_{\Delta}^{\star}))$":

We wish to prove $$ \mathcal{P}_\Delta = \text{Conv}(\Pi(\boldsymbol{P}_{\Delta}^*)) $$
because of the following:

> [!remark] 
> If a convex set is generated by the convex hull of a set of points $V$, then the extreme points of that convex set must necessarily belong to this set of points $V$.
> 


“It is easy to find that $P$ is the convex interpolation of $|\mathcal{I}|$ points in  
$\Pi\!\bigl(P^\star_{\Delta}\bigr)$ whose first $N$ coordinates are the same as $1-\Delta$  
and the $i$th coordinate is $1 - N(1-\Delta)$” ：对于集合 $\mathcal{I}$ 中的每一个索引 $i$，我们在极值点集合 $\Pi(\boldsymbol{P}_\Delta^*)$ 中选取一个特定的极值点 $\boldsymbol{E}_i$。这个极值点 $\boldsymbol{E}_i$：前 $m$ 个坐标等于 $1-\Delta$，第 $i$ 个坐标等于剩余概率 $R$，其余所有坐标等于 0。为每个 $\boldsymbol{E}_i$ 分配一个权重 $w_i = \frac{P_i}{R}$。对于前 $m$ 个坐标：$\sum_{i \in \mathcal{I}} w_i (1-\Delta) = (1-\Delta) \sum w_i = 1-\Delta$。与 $\boldsymbol{P}$ 一致。对于第 $j \in \mathcal{I}$ 个坐标：在所有选取的极值点中，只有 $\boldsymbol{E}_j$ 在这个位置非零。因此其值为 $w_j \cdot R = \frac{P_j}{R} \cdot R = P_j$。与 $\boldsymbol{P}$ 一致。对于其他坐标：恒为 0，与 $\boldsymbol{P}$ 一致。

In (a), for $$ \boldsymbol{P} = \theta \boldsymbol{P}_1 + (1-\theta) \boldsymbol{P}_2 $$
need a valid $\theta$. On $m$-th coordinates, $$ P_m = \theta (1-\Delta) + (1-\theta) \big(P_m + P_{m+1} - (1-\Delta)\big) $$
So $$ \theta = \frac{(1-\Delta) - P_{m+1}}{\big((1-\Delta) - P_m\big) + \big((1-\Delta) - P_{m+1}\big)} $$
which is in (0,1) as $1-\Delta > P_m \ge P_{m+1}$. Sub in $\theta$ to $m+1$ coordinates we also get $P_{m+1}$.








