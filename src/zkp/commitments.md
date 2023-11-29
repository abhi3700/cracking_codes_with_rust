# Commitments

## Cryptographic Commitments

A cryptographic commitment is a function that takes a message and a secret key and returns a commitment to the message. The commitment should be **binding**, meaning that it should be infeasible to find two messages that hash to the same commitment. The commitment should also be **hiding**, meaning that it should be infeasible to learn anything about the message from the commitment. [1](https://www.youtube.com/watch?v=IkNZWJFcfcU)

## Types

- Hash-based
  > Here, the hash function should be collision-resistant.
- Pedersen
  - It has an interesting property that it is additively homomorphic. E.g. `C(m1) * C(m2) = C(m1 + m2)` in short.

## Resources

- [Lecture 10.2: Cryptographic Commitments](https://www.youtube.com/watch?v=IkNZWJFcfcU)
