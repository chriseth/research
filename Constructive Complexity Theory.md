## Constructive Complexity Theory

### Constructive Separations

Mostly from "Constructive Separations and Their Consequences"

Definition Refuter (Kabanets, 2000): Let $\mathcal{L}$ be a language and $A$ be an algorithm.
An algorithm $R$ is a refuter for $\mathcal{L}$ against $A$ if it runs in polynomial time and
for all large enough $n$, $R(1^n)$ outputs an
$n$-bit string $x$ such that $\mathcal{L}(x) != A(x)$.

Definition Constructive Separation. To classes $\mathcal{A}$ and $\mathcal{B}$ have a
constructive separation if if there is a language $\mathcal{L}\in\mathcal{B}$
such that for all algorithms $A$ there is a refuter for $\mathcal{L}$ against $A$.

If "Palindromes is not in $NTIME_1[n^{1.1}]$" is constructive, then we get new circuit lower bounds.

### Bounded Arithmetic

Constructive proofs => refuters.

"PV": Defined by Cook. Contemporary extension: $PV_1$: binary strings, classical logic, no infinite sets.