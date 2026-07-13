> [!remark] 
> Let $X$ be a random variable with CDF $F_X(x) = \mathbb{P}(X \le x)$. 
> Let $U \sim U(0, 1)$. 
> Let $Y = F_X^{-1}(U)$, where $F^{-1}(p) = \inf \{ x \in \mathbb{R} : F(x) \geq p \}, \quad \forall p \in [0, 1]$.
> Then $Y\sim X$.

We see "unbiasedness" there.

##### How does it work?

**Imposing an Order on the Vocabulary**

The Inverse Transform method requires a 1D real number line to define a "Cumulative" function (i.e., you must be able to say $X \le x$). 

However, the vocabulary $\mathcal{W}$ is a set of words (categorical data) with no inherent mathematical order. 

To solve this, we introduce a permutation $\pi: \mathcal{W} \to \{1, 2, \dots, |\mathcal{W}|\}$. 
- $\pi(w)$ assigns a unique integer rank to a token $w$. 
- $\pi^{-1}(i)$ takes rank $i$ and returns the corresponding token. This permutation $\pi$ allows us to arrange the discrete probabilities of the NTP distribution $\boldsymbol{P}$ into a 1D sequence on the integer line. The probability of the token at position $i$ is $P_{\pi^{-1}(i)}$.

> [!remark] 
> Why need permutation?
> Even if we use some fixed ordering, inverse transform sampling still works and the watermark is still unbiased (intuitively, only the "length" but not the position matters).
> But we need this permutation to preserve security (if use some fixed order, then $w_{t}$ and the hidden pseudorandom number $U_{t}$'s coupling relationship are static and clear.) and more importantly, validity of the pivotal quantity under $H_{0}$. 
> 



**Deriving the CDF $F(x; \pi)$**

Consider the multinomial distribution with probability mass $P_{\pi^{-1}(i)}$ at $i$ for $1\leq i\leq \lvert \mathcal{W} \rvert$.

Now that the tokens are ordered from $1$ to $|\mathcal{W}|$, we can define the CDF. The CDF $F(x; \pi)$ is the cumulative sum of probabilities for all tokens assigned a rank less than or equal to $x$.

For any real number $x$: $F(x; \pi) = \sum_{i=1}^{\lfloor x \rfloor} P_{\pi^{-1}(i)}$

To express this in terms of the original vocabulary $\mathcal{W}$ rather than the integer indices, we sum over all tokens $w' \in \mathcal{W}$, but use an indicator function $\mathbf{1}_{\{\pi(w') \le x\}}$ to only include the probabilities of tokens whose rank is less than or equal to $x$.
$F(x; \pi) = \sum_{w' \in \mathcal{W}} P_{w'} \cdot \mathbf{1}_{\{\pi(w') \le x\}}$


**Deriving the Generalized Inverse $F^{-1}(U; \pi)$**

Because the distribution is discrete, the CDF $F(x; \pi)$ is a step function. we use the generalized inverse. For a uniform random variable $U \sim U(0,1)$, $F^{-1}(U; \pi) = \min \{ i \in \mathbb{Z} : F(i; \pi) \ge U \}$

Which is $F^{-1}(U; \pi) = \min \left\{ i : \sum_{w' \in \mathcal{W}} P_{w'} \cdot \mathbf{1}_{\{\pi(w') \le i\}} \ge U \right\}$


**Deriving the Decoder $\mathcal{S}^{\text{inv}}$**

$w_t = \mathcal{S}^{\text{inv}}(\boldsymbol{P}, \zeta) := \pi^{-1}(F^{-1}(U; \pi))$ where $\zeta = (\pi, U)$ and the permutation $\pi$ is uniformly at random.


**We show this watermark is unbiased.**

We need to show $\mathbb{P}(\mathcal{S}^{\text{inv}}(\boldsymbol{P}, \zeta) = w) = P_w$ for all $w \in \mathcal{W}$.

`Proof.`
Let $w$ be an arbitrary token in $\mathcal{W}$. Let its rank under the permutation be $k = \pi(w)$. Applying $\pi$ to both sides of $\pi^{-1}(F^{-1}(U; \pi))=\mathcal{S}^{\text{inv}}(\boldsymbol{P}, \zeta) = w$, equivalently $F^{-1}(U; \pi) = \pi(w) = k$.

And so equivalently $F(k-1; \pi) < U \le F(k; \pi)$.

Since $F(k; \pi) = \sum_{w' \in \mathcal{W}} P_{w'} \cdot \mathbf{1}_{\{\pi(w') \le k\}}$ and $F(k-1; \pi) = \sum_{w' \in \mathcal{W}} P_{w'} \cdot \mathbf{1}_{\{\pi(w') < k\}}$, then equivalently $$\sum_{w' \in \mathcal{W}} P_{w'} \cdot \mathbf{1}_{\{\pi(w') < k\}} < U \le \sum_{w' \in \mathcal{W}} P_{w'} \cdot \mathbf{1}_{\{\pi(w') \le k\}}$$
The length of this interval is $F(k; \pi) - F(k-1; \pi) = P_{\pi^{-1}(k)} = P_w$.

Since $U$ is uniformly distributed on the interval $(0, 1)$, then $\mathbb{P}(\mathcal{S}^{\text{inv}}(\boldsymbol{P}, \zeta) = w)=\mathbb{P}(F(k-1; \pi) < U \le F(k; \pi)) = P_w$.

Or we can use the first remark in this document.
$\mathbb{P}(X = i) = P_{\pi^{-1}(i)}$, if $Y = F_X^{-1}(U)$, then $Y\sim X$.
$\mathbb{P}(Y = i) = \mathbb{P}(X = i) = P_{\pi^{-1}(i)}$.
Note $\mathbb{P}(\text{output } w) = \mathbb{P}(Y = \pi(w))$, thus $\mathbb{P}(Y = \pi(w)) = \mathbb{P}(X = \pi(w)) = P_{\pi^{-1}(\pi(w))} = P_w$.
`QED.`






##### Main results

By "under $H_{1}$, in contrast, a larger $U_{t}$ value suggests a larger value of $\pi_{t}(w_{t})$ in distribution for the watermarked text, which can be gleaned from (23)", it means that: recall from above, we know if say $\pi_{t}(w)=k$, then token $w$ is chosen iff $F(k-1;\pi_{t})<U_{t}\leq F(k;\pi_{t})$.  

Typo above eqaution (37). Should be $\pi(l)=w$ not $\pi(l)=k$ in the index of summation.






##### Proof of Lemma 4.1

For $H_{0}$,  From $$\mathbb{P}(Y_t^{\text{dif}} \le r \mid H_0) = \sum_{w \in \mathcal{W}} \mathbb{P}\left(U_t \in [\eta(w) - r, \eta(w) + r] \cap [0,1], \pi_t(w_t) = w \mid H_0\right)$$
Use results from lemma C.1 for $H_0$: the joint probability is $\frac{1}{|\mathcal{W}|}$ multiplied by the probability of $U_t$ falling into the target interval. Because $U_t \sim U(0,1)$, the probability of $U_t$ falling into a specific interval within $[0,1]$ is exactly the length of that interval.

For $H_{1}$, note changed order of summation and replaced probability to uniform measure. 










