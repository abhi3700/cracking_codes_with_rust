# Elliptic Curve Cryptography

## Concepts

The ECC belongs to modern family of public-key cryptosystems. Elliptic curves are used in cryptography for key exchange and digital signatures. The maths of ECC is based on

- the algebraic structures of the elliptic curves over finite fields and
- the difficulty of the Elliptic Curve Discrete Logarithm Problem (ECDLP).

The ECC implements all major capabilities of the asymmetric cryptosystems:

- Encryption
- Digital signatures
- Key exchange

Now, why ECC is popular as most cryptosystems?

FYI, it was RSA previously, but as advances in computing power, the RSA is not secure anymore. So, ECC is the new standard for modern systems. And this is because of the following reasons:

- _smaller keys_ and _signatures_ than RSA for the same level of security
- provides _very fast key generation_, _fast key agreement_ and _fast signatures_.

### Private key

Let's understand the private keys in ECC. They are just random integers of x-bit. Now, x can be of any size. Example: `0x4df277becbfd6de16554ec65018997d6fba2ccf86c21274ad262fcccf8791be3` (32 bytes, hex encoded, 64 hex digits) of 256-bit secpk1256 curve. Now, this is the private key.

Generating private key is as simple as selecting a random integer within the given range. Suppose, with decimal base, we want to generate a 256-bit private key, then just select a random integer between `0` and `2ˆ256 - 1`. And then convert it to hex string.

> In terms of security, the only concern here is that the random number generator should be cryptographically secure.

Here are some examples of different curves that are named accordingly as per bit size:

- 192-bit (curve secp192r1),
- 233-bit (curve sect233k1),
- 224-bit (curve secp224k1),
- 256-bit (curves secp256k1 and Curve25519),
- 283-bit (curve sect283k1),
- 384-bit (curves p384 and secp384r1),
- 409-bit (curve sect409r1),
- 414-bit (curve Curve41417),
- 448-bit (curve Curve448-Goldilocks),
- 511-bit (curve M-511),
- 521-bit (curve P-521),
- 571-bit (curve sect571k1) and many others.

The most commonly used elliptic curve is **secp256k1** i.e. `yˆ2 = xˆ3 + a•x + b` in the field of digital signature (ECDSA) and key exchange (ECDH). Used in Bitcoin, Ethereum. Some networks use Ed25519 curve.

Are you thinking that only these are the possible curves? Well no, there are infinite curves possible. But, the above curves are standardized and hence used in practice as they are well studied and tested. There is no specific number of elliptic curves, as they can be defined over various fields, and their properties depend on the field they are defined over. In general, elliptic curves are curves defined by a certain type of cubic equation in two variables. EC have various applications in mathematics, including number theory, complex analysis, cryptography, and mathematical physics.

TODO: make notes on this: https://chat.openai.com/c/763b483d-308d-488e-9c5e-5d30c180d061

### Public key

Now, the public key is derived from this private key by multiplying the random number with a base point **𝘎** that lies on the EC. So, the scalar multiplication would result into private key point on EC.

Now, if you are thinking how to select **𝘎**, then let me give you some information.

> **𝘎** is typically predefined by the standards of the specific elliptic curve being used. It's chosen such that it generates a large cyclic subgroup, meaning that repeated addition of **𝘎** to itself covers a large portion of the points on the curve before repeating. The coordinates of **𝘎** and its order (the number of points in the subgroup it generates) are provided as part of the curve parameters in standards such as those specified by NIST or other cryptographic authorities.

Now, if you are thinking that the public key is of same size as private key. Then, you are mistaken. Actually, the public key has 1 more byte representing odd/even y-coordinate. Hence, there is a prefix added `02` or `03` in Ethereum's public key always. Here are some sample keypairs generated using secp256k1 curve:

```txt
Private key: 0x4df277becbfd6de16554ec65018997d6fba2ccf86c21274ad262fcccf8791be3
Public key: 0x038277e9975f31bd2d298632e88b4c91b7302af0159d4fe368a697200233714aa3

Private key: 0xd6911b2a64c378664f27ff0eef5f278ec8ca9325e80cd866fcc40293a920db64
Public key: 0x02b6ae10e60779ab44328893cdbddfec336ebc085c6857e733f3fd792be2b3ad5e
```

[Here](../../../libs/ecc/src/generate_keypair.rs) is the code example for generating keypair. Just run `$ cargo run`, it would print the keypairs labelled as `Private key` and `Public key`.

Please observe here that the public key starts with either `02` or `03` and then followed by 64 hex digits. The `02` or `03` represents the odd/even y-coordinate of the public key point on the elliptic curve. The compressed public key size is of 257 bit (leaving 0 as 4 bits).

## Applications

Two common use cases are:

- **ECDH** (Elliptic Curve Diffie-Hellman) is used for key exchange i.e. to share a secret key between two parties i.e. for Alice and Bob to share a secret key. `private_key_A * public_key_B = shared_secret_key = private_key_B * public_key_A`
- **ECDSA** (Elliptic Curve Digital Signature Algorithm) is used for digital signatures i.e. to sign a message digest using private key and then verify using public key, message and signature.

Some advanced use cases are:

- Using pairing friendly elliptic curves like BLS381, ec-pairing for ZKP, privacy preserving protocols etc.

- Bitcoin uses secp256k1 for digital signatures.
- Ethereum uses secp256k1 for digital signatures and key exchange.
- Zcash uses secp256k1 for digital signatures and key exchange.
- There is another family of elliptic curves called "pairing-friendly" i.e. **BLS** curves. These are used in ZKP (Zero Knowledge Proof) systems such as Zcash, Kogarashi Network, IoT security applications etc. E.g. BLS12-381 is based on ECC with an embedding degree of 12 and built over a 381-bit prime field GF(p).

## Code examples

1. Generate keypair. [Code example](../../../libs/ecp/src/generate_keypair.rs).
2. Sign message using private key and then verify using public key, message and signature. [Code example](../../../libs/ecp/src/verify_sig.rs).
3. Sign message digest using private key and then recover public key from recovery id, message digest, signature. [Code example](../../../libs/ecp/src/verify_sig_w_v.rs).
4. [ ] Encryption and Decryption using ECDH. [Code example](../../../libs/ecp/src/ecdh_enc_dec.rs).
5. [ ] Key exchange using ECDH. [Code example](../../../libs/ecp/src/ecdh.rs).
6. [ ] ZKP using BLS12-381. [Code example](../../../libs/ecp/src/bls12_381.rs).

## Coding

Normally, the keys (private, public) are in bytes array i.e. `[u8; 32]` in Rust. And the message is also in bytes array i.e. `[u8]` in Rust. And the signature is also in bytes array i.e. `[u8; 64]` in Rust.

But, we can also represent in hex string like `"027ee20ac1fb8cf19add3a5f7d8d1af8c5aedb7ff91f82130ad31811f4ad67591a"`.

The signatures are represented like this `CA2169BE0769A62C301B0BF482688B0E68916B02174F98E59AFB3269209714E21439E0A3808844A90AA0D92F905ED28696191B9B260A5905ABB46EBB34FE3A98` (64 bytes) and has r (32 bytes), s (32 bytes) components. And also another component called recovery id i.e. v, which is returned as 0 or 1 when the message digest is signed instead of message bytes using private key.
