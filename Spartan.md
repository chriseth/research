# Spartan

## Introduction

Can be used for R1CS.

R1CS: For given matrices $A, B, C$ over the finite field $\mathbb{F}$ is there a vector $w$ such that
$$(A \cdot w) \circ (B \cdot w) = C \cdot w\qquad \text{?}$$

Here, $\circ$ is element-wise multiplication.

In other words, for all $i$,
$$(A_i \cdot w) \cdot (B_i \cdot w) = C_i \cdot w,$$
where $M_i$ is the $i$th row of a matrix $M$.

In Spartan, the matrices are represented by functions $A \colon \{0,1\}^m \times \{0,1\}^m \mapsto \mathbb{F}$, where the first $m$ arguments index the row and the second $m$ arguments index the column of the matrix. Similarly, vectors are represented as $w\colon \{0,1\}^m \mapsto \mathbb{F}$.

Now we can write the same condition as

For all $x_i \in \{0,1\}$,
$F(\bar{x}) = (\sum_{y_i} A(\bar{x}, \bar{y}) \cdot w(\bar{y})) (\sum_{y_i} B(\bar{x}, \bar{y}) \cdot w(\bar{y})) - (\sum_{y_i} C(\bar{x}, \bar{y}) \cdot w(\bar{y})) = 0$.

Let $\tilde{F}$ be the multilinear extension of $F$.

So in order to check the condition, we can choose a random point $\tau$ and check that $\tilde{F}(\tau) = 0$. If the input field is large enough, this gives us high enough confidence.

## Spark

Protocol to evaluate the multilinear extension of a sparse function at a point given by the verifier.

Let $f\colon\{0,1\}^m\to\mathbb{F}$ be a sparse function, i.e. for some $r_1,\dots,r_n$ and $v_1,\dots,v_n$, we have $f(r_k)= v_k$ for $k=1,\dots,n$ and $f(x) = 0$ for $x \notin \{r_1,\dots,r_n\}$.

This means that
$$ \tilde{f}(x) = \sum_{k=1}^n v_k \cdot \mathrm{eq}(x, r_k)$$

Where $\mathrm{eq}$ is the multilinear function that is one when its two arguments are equal and zero otherwise. We abuse notation and use integers interchangeably with bitvectors.

This sum can be verified using the sum-check protocol. For that, we need to use the multilinear extension $\tilde{v}$ of the function $k \mapsto v_k$. This can/has to be computed by the verifier directly, but we can use a better technique for $\mathrm{eq}$: We use a lookup argument instead exploiting the structure inside $\mathrm{eq}$.