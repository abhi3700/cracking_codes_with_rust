# Shamir Secret Sharing

## Background

In digital world, we have passwords that can be used to access our accounts on different websites - Google, Facebook, Twitter, Apple. Right?

But what if our passwords/secret message/phrase is compromised or stolen during a data breach? We are doomed. Right?

## Concept

So, let's say we have a secret number (message encoded into a number) that we want to protect using SSSS. We can do this by using a technique called _Lagrange Interpolation_.

1. We first take any line that passes through this secret number.
2. Share any 2 points on this line with Bob and Charlie.
3. Now, let's say Bob and Charlie want to find the secret number without Alice's help. They can do this by sharing any 2 points on the line with each other and then finding the equation of the line passing through these 2 points and thus can find the secret number.

This is the problem with straight lines. They are easy to find. So, we use polynomials instead of straight lines to have more shares (pieces of secret) and thus more security.

---

1. Now, just like a straight line, in case of quadratic polynomial, there can be infinite number of quadratic polynomials passing through 2 points just like was the case with drawing straight lines through 1 point.
2. So, we need to share 3 points in order to have a unique quadratic polynomial passing through them. Hence, the min. threshold is 3.

But, just like straight lines, quadratic polynomials are also easy to find. So, we can go for cubic polynomials instead of quadratic polynomials to have more shares (pieces of secret) and thus more security.

---

And so on...

Hence, there comes Shamir Secret Sharing Scheme (SSSS) which is a _threshold scheme_. It is a form of _secret sharing_, where a secret is divided into parts, giving each participant its own unique part, where some of the parts or all of them are needed in order to reconstruct the secret.
It allows to define these:

- no. of shares
- threshold (min. no. of shares required to reconstruct the secret)
- modulus (prime no. used for arithmetic operations). Larger the modulus, more secure the scheme.

## Code

- [Seed recovery using ssss crate](https://github.com/abhi3700/subspace-auto/blob/main/sdk/examples/recover_seed_ph_ssss.rs)

## Resources

- [How to keep an open secret with mathematics using Shamir-Secret Sharing](https://www.youtube.com/watch?v=K54ildEW9-Q)
- [Simple introduction to Shamir's Secret Sharing and Lagrange interpolation](https://www.youtube.com/watch?v=kkMps3X_tEE)
- [Shamir's Secret Sharing - Solution and alternative to Lagrange](https://www.youtube.com/watch?v=rWPZoz0aux4)
- [Shamir Secret Sharing with No ID Numbers! by Jorge Arce-Garro | Devcon Bogotá](https://www.youtube.com/watch?v=7wcOPhBuIMw)
- [Bitcoin Q&A: Why is Seed Splitting a Bad Idea?](https://www.youtube.com/watch?v=p5nSibpfHYE)
- [Rust lib for Galois Field arithmetic with GF(2^256) i.e. 256-bit prime no.](https://github.com/geky/gf256) [RECOMMENDED]
- [Rust lib for GF(2^8) i.e. 8-bit prime no.](https://github.com/rustyhorde/sss)
