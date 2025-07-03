## Space Complexity of Circuit Evaluation

[Improved Bounds on the Space Complexity of Circutit Evaluation](https://eccc.weizmann.ac.il/report/2025/078), by Yakov Shalunov, 2025.

Main result: Size $s$ circuits can be evaluated in space $O(\sqrt{s \log s})$, "sibling"-result to [Wil25](https://eccc.weizmann.ac.il/report/2025/017/).

The main technique is grouping the gates in the circuit into blocks and mapping each block to a tree node for the TreeEval algorithm. The Circuit is also mapped to an exponentially-sized tree, but that is not a problem since the tree is not explicitly constructed.

There is another trick that subdivides the circuit graph into bocks such that the resulting coarse-grained graph has in-degree at most two, blocks of at most $b$ vertices and depth $d \cdot \frac{s}{b}$ for block size $b$.