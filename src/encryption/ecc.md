# Elliptic Curve Cryptography

## Concepts

Elliptic curves are used in cryptography for key exchange and digital signatures. The most commonly used is **secp256k1** i.e. `yˆ2 = xˆ3 + a•x + b` in the field of digital signature (ECDSA) and key exchange (ECDH).

Two common use cases are:

- **ECDH** (Elliptic Curve Diffie-Hellman) is used for key exchange i.e. to share a secret key between two parties i.e. for Alice and Bob to share a secret key. `private_key_A * public_key_B = shared_secret_key = private_key_B * public_key_A`
- **ECDSA** (Elliptic Curve Digital Signature Algorithm) is used for digital signatures i.e. to sign a message digest using private key and then verify using public key, message and signature.

Some advanced use cases are:

- Using pairing friendly elliptic curves like BLS381, ec-pairing for ZKP, privacy preserving protocols etc.

## Applications

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
