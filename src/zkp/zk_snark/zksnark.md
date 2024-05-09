# zkSNARK

zk-SNARK stands for zero-knowledge **S**uccinct (because of small proof size & lesser verification time) **N**on-interactive (no back & forth communication needed b/w prover & verifier) **AR**gument of **K**nowledge.

> - Succinct: small proof size & lesser verification time
> - Non-interactive: no back & forth communication needed b/w prover & verifier. This means when the prover submits the proof, the verifier can verify it without any further communication.

## Params

How to evaluate a scheme?

- proving time (lower the better)
- verification time (lower the better)
- proof size (lower the better)
- trusted setup size (with universal/different SCS (structured reference string) for each circuit) (lower the better)

## Circuits

They are essentially the mathematical equations which are mainly connected via arithmetic operations.

There are many languages by now to write the circuits. The most popular is circom.

In my opinion, it is not so likeable (by a Rustacean), hence I would personally opt for a Rust derived language - Noir, Leo, Halo2.

There is dedicated CLI tools for each while helps in compiling the circuits to its portable format (`.wasm`, `.r1cs`) files.

> Noir (developed by Aztec Protocol) compiles to ACIR (Abstract Circuit Intermediate Representation) which can then be further compiled to R1CS or an arithmetic circuit.
> Noir is a more of like an abstracted language. [ACIR](https://github.com/noir-lang/acvm/tree/master/acir) is written in Rust. I guess one can even write circuits in Rust using ACIR just like we write circuits in Rust using `arkworks-rs`.

## Schemes

There are many cryptographic schemes, each with its respective elliptic curve. The most popular is <u>_groth16 with BN256 curve_</u>. But recently, it has been found that the proof size is very high. Therefore, other schemes based on polynomial are getting more attention like KZG commitments with BLS12-381 curve, Plonk with BLS12-381 curve, etc.

Each combination aims to provide the best performance in terms of proving time, verification time, proof size, trusted setup size, etc.

Here is the list of schemes:

- Groth16 (smallest & fastest to verify)
- Libra
- Sonic
- SuperSonic
- PlonK
- SLONK
- Halo (Halo 2 ❌ trusted setup)
- Marlin
- Fractal
- Spartan
- Succinct Aurora,
- RedShift,
- AirAssembly

## Maths

If you are aiming to be a circuit developer, then you need to know the maths behind the schemes. Otherwise, you can just use the schemes as a black box.

<!-- TODO: Add more notes here -->

## Getting started

Following are the approaches I discovered so far:

1. From `Noir` lang perspective, I have tried by hands with [writing the circuits program in Noir](https://github.com/abhi3700/My_Learning_Cryptography/blob/main/proj/zkp/langs/noir) so far. Will take-up this course: [ZKCamp's Aztec Noir Course](https://github.com/ZKCamp/aztec-noir-course) blindly from theory to practical coding.
2. From `Rust` background, you can start with [first write some circuits using Rust with `arkworks-rs`](https://github.com/abhi3700/My_Learning_Cryptography/blob/main/proj/zkp/langs/arkworks/README.md) (groth16 scheme) & then switch to the other circuit langs as it doesn't make sense in the beginning to learn a new language just for writing circuits (unless you are a circuit developer).
3. If you come from NodeJS & Solidity, then hook onto `Circom` lang approach (also the traditional/conventional way), then watch these 2 videos in sequence: [Workshop - Learn Zero Knowledge Proofs (zkSNARKs), Circom, Snarkjs & Implement Solidity Dapp - 1](https://www.youtube.com/watch?v=1tw2wB5i9z8), [Workshop - Learn Zero Knowledge Proofs (zkSNARKs), Circom, Snarkjs & Implement Solidity Dapp - 2](https://www.youtube.com/watch?v=wYdzIwqZBQ0)

## Conclusion

## Resources

- [Lecture 10.3: What is a zk-SNARK?](https://www.youtube.com/watch?v=gcKCW7CNu_M)
