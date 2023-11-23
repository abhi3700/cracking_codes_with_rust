# zkSNARK

## Circuits

They are essentially the mathematical equations which are mainly connected via arithmetic operations.

There are many languages by now to write the circuits. The most popular is circom.

In my opinion, it is not so likeable (by a Rustacean), hence I would personally opt for a Rust derived language - Noir, Leo, Halo2.

There is dedicated CLI tools for each while helps in compiling the circuits to its portable format (`.wasm`, `.r1cs`) files.

> Noir (developed by Aztec Protocol) compiles to ACIR (Abstract Circuit Intermediate Representation) which can then be further compiled to R1CS or an arithmetic circuit.
> Noir is a more of like an abstracted language. [ACIR](https://github.com/noir-lang/acvm/tree/master/acir) is written in Rust. I guess one can even write circuits in Rust using ACIR just like we write circuits in Rust using `arkworks-rs`.

## Getting started

I have although tried [writing the circuits program in Noir](https://github.com/abhi3700/My_Learning_Cryptography/blob/main/proj/zkp/langs/noir) so far. But I guess, it would be nice to [first write some circuits using Rust with `arkworks-rs`](https://github.com/abhi3700/My_Learning_Cryptography/blob/main/proj/zkp/langs/arkworks/README.md) & then switch to the other circuit langs as it doesn't make sense in the beginning to learn a new language just for writing circuits (unless you are a circuit developer).

## Conclusion
