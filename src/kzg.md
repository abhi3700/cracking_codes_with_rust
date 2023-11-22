# KZG Commitments

If you are curious, why KZG, then refer to the [FAQs](#faqs) section first.

## FAQs

**Q**. Why KZG?

**A**. They can replace Merkle Tree variants (like Merkle Mountain Range (MMR), Merkle Patricia) with a _constant size_ proof (48 bytes). The merkle proof size grows with the number of leaves in the tree. KZG commitments are _constant size_.

---

**Q**. Does KZG follow normal polynomial? If not what it is and Why do we need a different polynomial?

**A**. No, here polynomials are defined over a finite field. This means that when doing arithmetic operations on the coefficients, the result is always reduced modulo the field's characteristic. For instance, each coefficient is an element of the field Fp, where p is a prime number. For more view [examples](#code).

<details>
<summary>Details:</summary>

E.g. `f(x) = 3x^2 + 2x + 1` is a polynomial over a finite field Fp, where p is a prime number. Here, the coefficients are 3, 2, 1. The degree of the polynomial is 2.
g(x) = 2x^2 + 1 is also a polynomial over a finite field Fp, where p is a prime number. Here, the coefficients are 2, 0, 1. The degree of the polynomial is 2.

When we add them, we get `f(x) + g(x) = 5x^2 + 3x + 2`. Here, the coefficients are 5, 3, 2. The degree of the polynomial is 2. This happens in case of normal polynomials. But, with FF, the coefficients are reduced modulo the field's characteristic.

> Although the result with FF would also be same in this case as the sum result is within the large prime number (if considered as boundary).

Now, why do we need to define a normal polynomial over FF?

To construct commitments to these polynomials. The KZG scheme allows for efficient proofs of certain properties of the polynomial (like polynomial evaluations) without revealing the polynomial itself. Hence, has similar properties to a Merkle Tree.

Analogy:

| Merkle Tree              | KZG Commitments                        |
| ------------------------ | -------------------------------------- |
| Leaf                     | Polynomial coefficients                |
| Root                     | Polynomial commmitment i.e. polynomial |
| Proof                    | Proof                                  |
| growing size with leaves | constant size i.e. 48 bytes            |

</details>

---

## Maths

<!-- TODO: -->

## Code

There is a repo: [rust-kzg](https://github.com/sifraitech/rust-kzg) with 2 packages:

```toml
kzg = { git = "https://github.com/sifraitech/rust-kzg.git", package = "rust-kzg-blst" }
kzg_traits = { git = "https://github.com/sifraitech/rust-kzg.git", package = "kzg" }
```

Here, the `kzg` is called for the rust-kzg-blst package and `kzg_traits` is called for the kzg package of the [repo](https://github.com/sifraitech/rust-kzg).

Some [examples](https://github.com/sifraitech/rust-kzg/libs/kzg_cookbook/examples/) based on polynomials.

The examples are based on KZG polynomials i.e. polynomials defined over a finite field.

### Create a polynomial (from given len, zero coefficients)

All coefficients are set to zero by default.

[Code](https://github.com/abhi3700/My_Learning_Cryptography/blob/main/libs/kzg_cookbook/examples/create_poly_zcoeff.rs)

### Create a polynomial (from given coefficients)

[Code](https://github.com/abhi3700/My_Learning_Cryptography/blob/main/libs/kzg_cookbook/examples/create_poly_coeff.rs)

### Create a polynomial (from random coefficients)

[Code](https://github.com/abhi3700/My_Learning_Cryptography/blob/main/libs/kzg_cookbook/examples/create_poly_rand.rs)

<!-- TODO: ## Evaluate a polynomial at a point -->

<!-- TODO: ### Add 2 polynomials -->

## Resources

### Videos

- [KZG POLYNOMIAL COMMITMENTS by OpenSense Research](https://www.youtube.com/watch?v=h7yKGYt391M&list=RDCMUC_iWxlRBCbg0my5J9MZPVYA&start_radio=1) 🧑🏻‍💻
