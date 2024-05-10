#### KZG

Relies on structured reference string consisting of $ S= ( g, g^{\tau}, \dots, g^{\tau^{n-1}}) $ for some $g \in \mathbb{F}$ and $\tau$, where $\tau$ is assumed to be unknown to the prover and verifier.

It also requires an elliptic curve that has a pairing $e$.

**Commitment** to polynomial $f \in \mathbb{F}[X^n]$ is $$c := g^{f(\tau)},$$ which can be computed using $S$.

Note that $S$ only allows commitments to polynomials of degree at most $n$, which is a benefit, since it is a built-in low-degree check.

**Evaluation proof** of the statement $f(z) = u$:

Note that $$q(X) := \frac{f(X) - u}{X - z}$$ is a polynomial if and only if $f(z) = u$.

So the prover computes and sends $y := g^{q(\tau)}$.

The verifier checks
$$ e(c  g^{-u}, g) = e(y, g^\tau  g^{-z}) $$
using the pairing $e$.

**Completeness**:

LHS:
$$ e(c  g^{-u}, g) = e(g^{f(\tau)}  g^{-u}, g) = e(g^{f(\tau)-u}, g) $$
RHS:
$$ e(y, g^{\tau-z}) = e(g^{q(\tau)}, g^{\tau - z}) =e(g^{\frac{f(\tau) - u}{\tau - z}}, g^{\tau - z}) $$

**Soundness**: Sketch: If $f(z) \neq u$, then $q$ is not a polynomial. This means that without knowing $\tau$, the $y$ that the prover sends cannot be equal to $g^{q(\tau)}$.