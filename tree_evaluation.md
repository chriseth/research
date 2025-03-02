## Tree-Evaluation

### Problem statement

Given a complete binary tree of height $h$ whose leafs are labeled with $b$-bit strings and inner nodes labeled with functions mapping two of those to one (given as a table), compute the recursively defined value at the root.

The length of the input is $n = (2^h - 1)(2^{2b} b) + 2^hb = \mathrm{exp}(\Theta(h + b))$.

Evaluating the tree in depth-first order yields a space complexity of $O(h \cdot b)$. Solving the problem in logarithmic space would mean in $O(h + b)$.

### Polynomial Interpolation

(taken from the [exposition by Goldreich](https://www.wisdom.weizmann.ac.il/~oded/COL3/tree-eval.pdf))

Using polynomial interpolation, Cook and Mertz [CM24](https://doi.org/10.1145/3618260.3649664) showed that the problem can be solved in $O(b + h \log b)$ space.

Let $\mathbb{F}$ be a field of characteristic $2$ such that $|\mathbb{F}| \ge 2b + 2$. TODO

Let $f_{u,j}\colon \{0,1\}^{2b} \to \{0,1\}$ be the function that returns the $j$-th bit of the value computed in node $u\in \{0,1\}^{\le h}$. Let $\widehat{f_{u,j}}\colon \mathbb{F}^{2b} \to \mathbb{F}$ be the multilinear extension of $f_{u,j}$. TODO How is this defined exactly?

In the recursive algorithm, we want to use occupied memory locations but reset to their original value before we return. We do so by computing evaluation points of some multilinear function at many points in the field on certain variations of those occupied memory locations. We will then use those points to interpolate the function and evaluate it at the origin, which allows us to compute the value undisturbed.

For any $u \in \{0,1\}^{\le h}$, let $v_u$ be the value computed in node $u$, i.e. $v_u = f_u(v_{u0}, v_{u1})$ if $|u| < h$ and $v_u$ is taken from the input if $|u| = h$.

Let $\omega \in \mathbb{F}$ be an $m$ th root of unity.

We describe a recursive procedure. On input $(u, x, y, z)\in \{0,1\}^{\le h} \times \mathbb{F}^{3b}$, we want to return $(u, x, y, z + v_u)$. For the inputs and outputs we use the same memory location during the whole recursion.

We start out with the input $(u, x, y, z) = (u, x, y, z_0)$.

For $j = 0, 1, \dots, m - 1$, do:
- Make a recursive call to $(u0, z_j, y, \omega^jx)$ to get $(u0, z_j, y, x')$, where $x' = \omega^jx + v_{u0}$.
- Make a recursive call to $(u1, z_j, x', \omega^jy)$ to get $(u1, z_j, x', y')$, where $y' = \omega^jy + v_{u1}$.
- Compute $z_{j+1} = z_j + (\widehat{f_{u,0}}(x', y'), \widehat{f_{u,1}}(x', y'), \dots, \widehat{f_{u,b-1}}(x', y'))$.
- Make a recursive call to $(u0, z_{j+1}, y', x')$ to get $(u0, z_{j+1}, y, w^j x)$ (note that $\mathbb{F}$ has characteristic $2$).
- Make a recursive call to $(u1, z_{j+1}, x, y')$ to get $(u1, z_{j+1}, x, w^j y)$.

Observe that for all $i=0,\dots,b-1$, we have  $(z_m)_i = (z_0)_i + \sum_{j = 0}^{m-1} \widehat{f_{u,i}}(\omega^j x_i, \omega^j y_i) = \widehat{f_{u,i}}(x_i, y_i)= f_{u,i}(x_i, y_i)$ by Lemma 1. Thus, $z_m = v_u$ and we can return $(u, x, y, z + v_u)$.


Note that the above algorithm uses one field element per bit. To get the full statement, we have to be a bit more clever and use group multiple bits into one element of the field, but respecting all bounds properly.


### Lemma 1

Let $\omega$ be an $m$-th root of unity in $\mathbb{F}$ and $m < |F|$. Let $p\colon\mathbb{F}^n \to \mathbb{F}$ be a polynomial of degree $d < m$. Then for all $\tau_1,\dots,\tau_n,x_1,\dots,x_n\in\mathbb{F}$

$$ \sum_{j=1}^m p(\omega^j x_1, \dots ,\omega^j x_n) = m \cdot p(x_1,\dots,x_n) $$

Proof:




, then for any $i \in \{0,1\}^{2b}$ and $j \in \{0,1,\dots,m-1\}$, we have $\sum_{j = 0}^{m-1} \omega^{ij} = 0$ if $i \ne 0$ and $\sum_{j = 0}^{m-1} \omega^{ij} = m$ if $i = 0$.


----

|S| = 2 ^(q/2) = 2^(1 + log b)
t = 2b / q,
q  = log(4b^2) = 2 + 2 log b
t = b / (1 + log b) = |F|

Check: How much space do we actually need for what?


TODO:
- What are the bounds on $m$ (the order of $\omega$)?
- What are the size bounds on the field? Cook-Mertz only need cardinality $2b + 2$.
- Somewhere I read that the values are not computed bit-wise but as field elements. Where was that?


-----

As presented by goldreich.

Space efficient algorithm for tree eval problem.
Given complete binary tree with l-bit labeled leafs and inner nodes labeled with functions mapping two of those to one (given by truth table), compute the recursively defined value at the root.

Key insight: use linearity (multilinear extensions) and reversible computation to store many different values in the same memory cell.

More specifically: keep global memory of three values x, y, z. On input of path u and x, y, z, we compute x, y, z + v_u, where v_u is the value computed in node u, v_u = f_u(v_u0, v_u1) Note that x and y are just returned unchanged. We do this as follows:
Recursively call on u0, y, z, x to get x‘=x+v_u0
Recursively call on u1, x‘, z, y to get y‘=y+v_u1
Now in fact we use multilinear extensions instead of direct values. So in fact we do this for many different x with the effect that we can accrue values in z that also contain components of x and y but those will cancel out in the end (think of summing roots of unity or interpolating polynomials), leaving only the always unchanging v_u component. We also always undo the computation by reversing the signs so that we get the original x and y back. In the end we will have z + v_u

The solution is calling the routine on "", 0, 0, 0



