# Montgomery Modular Multiplication

A method to reduce the cost of computing the remainder mod $N$ after multiplying two numbers $a$, $b$.

The drawback is that turning a regular integer into montgomery form has a certain cost, so it is only beneficial if multiple operations are performed in montgomery form.

The idea is to use a different "modulus", $R$, which is usually a power of two larger than $N$ and compute the remainder mod $R$ is trivial.

We also precompute the inverse of $R$ mod $N$, so $R$ must be coprime to $N$.

The montgomery form of $a$ is $aR \bmod N$. Addition and subtraction are done as usualy with just one subtraction / addition of $N$ after the operation.

Multiplication cannot be done directly, because

$(aR \bmod N)(bR \bmod N) \equiv_N (aR \bmod N)(bR \bmod N) \equiv_N abRR $

has an additional factor of $R$. We can remove it by multipliyng with the precomputed $R^{-1} \pmod N$, but that requires an additional multiplication and especially reduction modulo $N$, so we did not gain anything.

The key insight is the montgomery reduction, which computes the product with $R^{-1} \pmod N$ and reduces mod $N$ at the same time:

For this, we precompute some $N'$ such that $NN' \equiv_{R} -1$.

Then, on input $x \leq RN - 1$ we compute:

\[
\begin{align}
    m &= (x \bmod R)N' \bmod R\\
    y &= (x + mN) / R\\
    \texttt{if } y &\geq N \texttt{ \{ } y - N \texttt{ \} else \{ } y \texttt{ \}}
\end{align}
\]

The idea behind computing $m$ is that it is meant to cancel the residue modulo $R$: it makes $x + mN$ divisible by $R$:

$x + mN \equiv_R x + (x \bmod R)N'N \equiv_R x - (x \bmod R) \equiv_R 0$

This means that $y$ can be simply be computed using integer arithmetic.

Sice $m$ is in $\{0,1,...,R-1\}$, the value of $y$ is at most $2N - 1$.

Finally, $y \equiv_N x R^{-1}$ because

\[
    y \equiv_N (x + mN) / R \equiv_N xR^{-1} + mNR^{-1} \equiv_N xR^{-1}
\]
