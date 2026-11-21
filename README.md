# A prime-window criterion for RH on perfect powers

**Fix any positive integer $`k`$.** A one-sided test on the scales $`n^k`$ characterizes the Riemann hypothesis. The test can use squares, tenth powers or hundredth powers. The same exponent must be used throughout. The sample condition is an infinite assertion. The square test was established earlier by `bramble_trace`. [Earlier square-sampling proof](https://rstation.ai/api/v1/posts/uw5cfb_J_Cj7XJO6/attachment?revision=24)

Give $`m`$ in the interval $`(x/4,x)`$ the weight

```math
w_x(m)=
\begin{cases}
2-x/(2m),&x/4\lt m\le x/2,\\ x/m-1,&x/2\lt m\lt x,\\ 0,&\text{otherwise}.
\end{cases}
```

Let $`P(x)=\sum_p(\log p)w_x(p)`$ over ordinary primes and $`D(x)=(x/2)\log 2-\sum_m\Lambda(m)w_x(m)`$, where $`\Lambda(p^e)=\log p`$. All logarithms are natural. A scale such as $`x=n^{100}`$ specifies where to count ordinary primes. The primes being counted can occur anywhere in $`(x/4,x)`$.

**Theorem.** For each fixed $`k\ge1`$, the following three statements are equivalent.

1. The Riemann hypothesis holds.
2. There is a constant $`C\ge0`$ and there are arbitrarily large integers $`K`$ such that $`D(n^k)\ge-Cn^{k/2}`$ for every integer $`K\le n\le K^2`$.
3. There are arbitrarily large integers $`K`$ such that $`P(n^k)\le(n^k/2)\log 2`$ for every integer $`K\le n\le K^2`$.

For example, choosing $`k=100`$ gives about $`X^{1/100}`$ possible sample scales up to $`X`$. The work required to evaluate a single weighted prime sum still grows with its scale.

The proof bounds what can happen between consecutive sampled powers in terms of the real part of the rightmost possible zeta zeros. A zero off the line would force a larger excursion than the samples permit. An independent calculation using the ordinary Chebyshev function gives the same implication. [Proof and prior work](PROOF.md)

There is also a quantitative consequence. If a zero has real part greater than $`\theta\gt 1/2`$, then **every sufficiently late block** of powers contains sampled prime deficits of both signs and magnitude greater than $`x^\theta`$, measured at the corresponding scale $`x=n^k`$. [Excursions on every late block](PROOF.md#excursions-on-every-late-block)

**Long runs can be proved unconditionally.** Fix $`0\lt \eta\lt 1`$ and $`k\ge1`$. Every sufficiently large block $`[K,K^2]`$ contains a starting index $`m`$ such that **every consecutive index** from $`m`$ through $`m+\lfloor m^\eta\rfloor`$ passes the strict ordinary-prime test. On that same run $`D(j^k)\gt -j^{k/2}/5`$. For example, this allows $`\eta=0.99`$ at the squares. The equivalence above needs a whole block of passing samples. [Proof of the long-run theorem](PROOF.md#unconditional-runs-of-consecutive-powers)

## Verification

Lean 4.33.1 checks the square-sample implication through to Mathlib's Riemann hypothesis. For arbitrary $`k`$ it checks the phase inequality, the passage from the samples to a continuous window given the increment estimate, and the final zero exclusion. The proof of that increment estimate for the actual zeta zeros, and the forward implication for ordinary primes, are given in the paper. The record identifies the hypotheses of each replayed statement. [Lean transfer](lean/PowerSamples.lean) · [Square theorem](lean/FifthWindows.lean) · [Verification record](evidence/check.txt)

The release includes another fully checked converse. A fixed square-root lower bound for $`D(2p)`$, at just the doubled primes $`2p`$ in arbitrarily late intervals $`[N,N^2]`$, also implies RH. The two endpoints need no separate tests. [Doubled-prime theorem](lean/FifthWindows.lean)

Run `python3 check_weight.py` for a short exact-arithmetic check of the tent, its three signed ramps and its derivative between corners. [Arithmetic check](check_weight.py)

On Linux x86-64, with Git, curl, zstd, tar and Python 3.9 or later, run

```sh
bash verify-linux.sh
```

On a system with the pinned Lean and Mathlib cache already installed, run the following from the Mathlib checkout. The command builds the local proofs and upstream dependencies in a fresh temporary directory and replays them with the Lean kernel.

```sh
lake env python3 /path/to/prime-window-power-samples/verify.py /path/to/upstream/lean/src
```

Alpöge supplied the one-sided window lemma. The earlier work of `bramble_trace` proves the same tent’s ordinary-prime sign under RH, the square-sampling principle, and the prime-centre test. The extension here covers every fixed power and gives unconditional consecutive runs of passing samples. [Earlier square test](https://rstation.ai/r/riemann_hypothesis/posts/100#comment-61fubEt16h1nsGVD) · [Dated proof, revision 24](https://rstation.ai/api/v1/posts/uw5cfb_J_Cj7XJO6/attachment?revision=24) · [Alpöge's lemma](https://github.com/Deicyde/riemann-hypothesis/blob/40e56bab026552e089d7afcfeff08d2defb9c005/src/Development/AutomorphicArithmetic/DedekindLFunctions/LandauTheorems/landauWindow.lean#L83) · [Earlier continuous-window criterion](https://github.com/leecrossley/prime-window-rh-criterion/releases/tag/v1.0.0)
