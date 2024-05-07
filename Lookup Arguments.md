## Lookup Arguments

**Vector:** ordered list of field elements

**Zero-Check:** check that all elements of a vector are zero

**Sum-Check:** check that the sum of the elements of a vector is equal to a certain field element


### Permutation Check

Want to check that $A = (a_1, \dots ,a_n)$ and $B = (b_1, \dots, b_n)$ are permutations of each other.

Observation: This is true if and only if the following polynomials are identical:

$$p_A(X) = \prod_{i=1}^n (X - a_i) \qquad
p_B(X) = \prod_{i=1}^n (X - b_i)$$

**Idea:** Check the evaluation of the two polynomials at a random point. We do this using
a so-called "grand product argument":

We can check $\frac{p_A(\beta)}{p_B(\beta)} = 1$ iteratively by addig a witness column $z$ and a random challenge $\beta$ with the following constraints:

$z_1 = 1$,
$z_{i+1} = z_i \frac{\beta - a_i}{\beta - b_i}$

The actual check is achieved by the cyclic nature of the constraints.

### Halo2 Lookup Argument

We show $A \subseteq B$ by computing a permutation $X$ of $A$ and a permutation $Y$ of $B$ such that for each $i$,

$X_{i+1} = X_i$ or $X_{i+1} = Y_{i+1}$.

Idea: If $X$ changes, then it has to be equal to $Y$, i.e. $Y$ has to change at least as often as $X$.

### Lookup Argument via Product Check: LOGUP

To show $A \subseteq B$, show 

#$ \prod_{i=1}^n (X - a_i) = \prod_{i=1}^n (X - b_i)^{m_i} $$

where $m_i$ is the multiplicitiy of $b_i$ in $A$ (which can be zero).

If we now take the logarithm on both sides, this turns into

$$ \sum_{i=1}^n \log(X - a_i) = \sum_{i=1}^n m_i \log (X - b_i) $$

And as a next step, we can take the derivative:

$$ \sum_{i=1}^n \frac{1}{X - a_i} = \sum_{i=1}^n \frac{m_i}{X - b_i} $$

This representation is equivalent as long as the size of the sets is less than the
characteristic of the field.

So in the end we turned the product check into a sum check.

We implement this by committing to the vectors and the multiplicities. Then we compute the sum iteratively.

So in the end we only need two additional columns.

### Logup + GKR

By implementing fractions through their numerator-denominator representation, we do not have to commmit to the helper column. Instead, we comute the sum in a layered circuit.
