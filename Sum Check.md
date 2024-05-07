## Sum-Check Protocol

Origin: [LFKN92: Algebraic Methods for Interactive Proof Systems](https://dl.acm.org/doi/pdf/10.1145/146585.146605)

Every language in the polynomial hierarchy has an interactive proof system.

The original proof gave an interactive protocol for the permanent
of 0-1-matrices, which is a #P-complete problem. Together with a
theorem by Toda, we get the stated result.

The Sum-Check Protocol is an interactive protocol to compute

$$ \sum_{b \in \{0,1\}^v} g(b), \qquad \text{for } g \in \mathbb{F}[X_1,\dots,X_v] $$

where the verifier has oracle access to $g$.

### Protocol

#### Round 1:

Prover sends $H$ (the claimed sum) and

$$ g_1(X_1) = \sum_{b \in \{0,1\}^{v-1}} g(X_1, b). $$

Verifier checks that $g_1$ has the correct degree and checks $H = g_1(0) + g_1(1)$.

Verifier sends a random $r_1 \in \mathbb{F}$.

#### Round $j$, $1 < j < v$:

Prover sends

$$ g_v(X_v) = \sum_{b \in \{0,1\}^{v-j}} g(r_1, \dots, r_{v-1}, X_v, b). $$

Verifier checks that $g_v$ has the right degree and that $g_{v-1}(r_{v-1}) = g_v(0) + g_v(1)$.

Verifier sends a random $r_j \in \mathbb{F}$.

#### Round $v$:

Verifier chooses a random $r_v \in \mathbb{F}$ and verifies that $g_{v-1}(r_{v-1}) = g(r_1,\dots, r_v)$.

This is the only step where oracle access to $g$ is needed, the other computations were all done on (low-degree) univariate polynomials.

### Correctness

Correctness is evident.

### Soundness

