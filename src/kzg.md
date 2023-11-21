# KZG Commitments

**Q**. Why KZG?

**A**. They can replace Merkle Tree variants (like Merkle Mountain Range (MMR), Merkle Patricia) with a _constant size_ proof (48 bytes). The merkle proof size grows with the number of leaves in the tree. KZG commitments are _constant size_.

## Maths

## Code

There is a repo: [rust-kzg](https://github.com/sifraitech/rust-kzg) with 2 packages:

```toml
kzg = { git = "https://github.com/sifraitech/rust-kzg.git", package = "rust-kzg-blst" }
kzg_traits = { git = "https://github.com/sifraitech/rust-kzg.git", package = "kzg" }
```

Here, the `kzg` is called for the rust-kzg-blst package and `kzg_traits` is called for the kzg package of the [repo](https://github.com/sifraitech/rust-kzg).

Some [examples](https://github.com/sifraitech/rust-kzg/libs/kzg_cookbook/examples/) based on polynomials.

## Resources

### Videos

- [KZG POLYNOMIAL COMMITMENTS by OpenSense Research](https://www.youtube.com/watch?v=h7yKGYt391M) 🧑🏻‍💻
