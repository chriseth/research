## Sum-Check Protocol

Origin: [LFKN92: Algebraic Methods for Interactive Proof Systems](https://dl.acm.org/doi/pdf/10.1145/146585.146605)

Every language in the polynomial hierarchy has an interactive proof system.

The original proof gave an interactive protocol for the permanent
of 0-1-matrices, which is a #P-complete problem. Together with a
theorem by Toda, we get the stated result.

The Sum-Check Protocol is an interactive protocol to compute

$$ \sum_{b \in \{0,1\}^v} g(b), \qquad \text{for } g \in \mathbb{F}[X_1,\dots,X_v] $$

where the verifier has oracle access to $g$. It has a completeness error of zero and a soundness error of at most $\frac{v\,\mathrm{deg}(g)}{|\mathbb{F}|}$.

### Protocol

Let $g_0(X)$ be a constant polynomial that is the claimed sum and let $r_0 = 0$.

#### Round $j \in \{1, \dots, v-1\}$:

Prover sends

$$ g_v(X_v) = \sum_{b \in \{0,1\}^{v-j}} g(r_1, \dots, r_{v-1}, X_v, b). $$

Verifier checks that $g_v$ has the right degree and that
$$ g_v(0) + g_v(1) =  g_{v-1}(r_{v-1}) $$

Verifier sends a random $r_j \in \mathbb{F}$.

#### Round $v$:

Verifier chooses a random $r_v \in \mathbb{F}$ and checks that $g_{v-1}(r_{v-1}) = g(r_1,\dots, r_v)$.

This is the only step where oracle access to $g$ is needed, the other computations were all done on (low-degree) univariate polynomials.

### Correctness and Soundness

Correctness is evident, soundness can be shown by induction on the number of rounds using the Schwartz-Zippel lemma.

### Cost analysis

Ignoring the cost for the polynomial commitment, the prover sends $\mathrm{deg}(g)$ field elements, the verifier $v$, so the communication complexity is $O(\mathrm{deg}(g))$, which is also the bound on the runtime of the verifier.

Concerning the runtime of the prover, in round $j$, the prover needs to compute a sum of $2^{v - j}$ polynomial evaluations. in total, these are
$$ \sum_{j = 1}^v 2^{v - j} = O(2^v). $$