# Linear Codes

From [Succinct Proofs and Linear Algebra](https://angeris.github.io/papers/zk-linalg.pdf) by Evans and Angeris.

### Definitions

#### Vandermonde Matrix

The Vandermonde Matrix of degree $n -1$ for the evaluation points $\alpha_1, \dots, \alpha_m$ is

$$ A = (\alpha_i^{j - 1})_{ij} = \begin{bmatrix}
1 & \alpha_1 & \alpha_1^2 & \cdots & \alpha_1^{n-1} \\
 &  & & \vdots &  \\
1 & \alpha_m & \alpha_m^2 & \cdots & \alpha_m^{n-1} \\
 \end{bmatrix} $$

Its range is the vector space of evaluations of all polynomials of degree at most $n-1$
at the points $\alpha_1, \dots, \alpha_m$.

#### Linear Codes

Every matrix $G \in F^{m \times n}$ defines a linear code with message length $n$ and
block length $m$. Its distance is defined as
$$
d = \min_{x \in F^n\setminus\{0\}} || G x ||_0.
$$
Any two different messages will be encoded into codewords that differ in at least $d$ entries.

A code with high distance allows us to detect errors by checking only some of the places
in the codeword.

#### Reed-Solomon Code

The Vandermonde matrix is used for Reed-Solomon codes. These codes have distance $m - n + 1$
because polynomials with degree at most $n - 1$ have at most $n - 1$ zeros.

##### Notes on Practical Implementations

In practice, the evaluation points usually are _all_ elements of the finite field,
since the matrix is never explicitly constructed, but a challenge-response system is used instead.
The large distance value is achieved because the field is usually _large_ and the polynomial
degree is _small_.