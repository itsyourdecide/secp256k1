# secp256k1 from scratch in Rust

I decided to write my own implementation of the secp256k1 elliptic curve. This is the very foundation that Bitcoin and Ethereum run on.

Everything is built completely from scratch. I didn't use any ready-made cryptographic libraries or BigInt — just pure Rust and mathematics. This project is a continuation of my work on SHA-256.

## The Journey

For me, this was a great opportunity to practice. I had to recall school-level long multiplication and subtraction, but this time at the level of massive 256-bit numbers.

Generally, I'm more used to analytical mathematics, so discrete algebra was new to me, but I got the hang of it pretty quickly. In reality, there's no crazy magic here. If you have enough patience, anyone can wrap their head around the code and the math. For those who want to dig deeper, I can provide links to the sources I used. I'll also attach my Paint sketches — they contain the pure theory and calculations I made during the process. Feel free to look for easter eggs in them.

## What's inside

- U256 Arithmetic: my own implementation of 256-bit integers, split into four 64-bit blocks.
- U512 Multiplication: honest multiplication of two 256-bit numbers resulting in a 512-bit value.
- Modular Reduction: fast reduction modulo p, leveraging the specific structure of the Koblitz curve.
- Fermat's Inverse: finding the modular multiplicative inverse using the formula $a^{p-2} \pmod p$.
- Curve Geometry: point addition and doubling in affine coordinates.
- Scalar Multiplication: the Double-and-Add algorithm for calculating $k * G$.
- Validation: checking that the private key is non-zero and doesn't exceed the curve order n.

## Important Note

This code was written for educational purposes only.

Nobody has audited the security.

Do not even think about using this for real money or storing actual keys.

## How to run

```bash
cargo run
```

You'll see something like this in the console:

```text
Private Key: 18e14a7b6a307f426a94f8114701e7c8e774e7f9a47e2c2035db29a206321725
--- RESULT ---
Public Key X: 50863ad64a87ae8a2fe83c1af1a8403cb53f53e486d8511dad8a04887e5b2352
Public Key Y: 2cd470243453a299fa9e77237716103abc11a1df38855ed6f2ee187e9c582ba6
```

## Project Structure

- src/secp256k1.rs — the mathematical core: numbers and curve logic.
- src/main.rs — an example of how it all works in practice.
