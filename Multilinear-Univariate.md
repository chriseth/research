## Implementing Multilinear Polynomial Commitment Schemes using Univariate Ones

Some potentially relevant resources: [Nam23](https://arxiv.org/pdf/2306.11383): A Survey of Multivariate Polynomial Commitment Schemes

[Gemini](https://eprint.iacr.org/2022/420.pdf) added to KZG seems to give a multilinear commitment scheme.

The [Lasso](https://people.cs.georgetown.edu/jthaler/Lasso-paper.pdf) article is a good resource in general.


Fixing the first variable of a multilinear polynomial to $r$ is the same as splitting the corresponding univariate polynomial $f$ into odd and even parts $f_o$ and $f_e$ such that $f(X) = f_e(X^2) + X f_o(X^2)$ and using $f_e(X) + r f_o(X)$.

