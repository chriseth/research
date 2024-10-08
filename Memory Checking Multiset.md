# Memory Checking using Multiset

Talk by Jens Groth at zkSummit 12. Uses constant amount of field ops and thus
comparable to other current techniques.

Use multiset hash function to do offline memory checking.

Multiset hash function: Easy to compute hash of multiset-union.

Example: Hash function to group for singletons and sum over singletons.
(uses discrete log)

Check memory by iteratively computing hash of reads and hash of writes (like in offline memory checking) and check that the hash is the same at the end.

Idea: Instead of hash function just use injective function to a group if values are "small" enough.

Use some other coordinate so that they satisfy an elliptic curve equation.w