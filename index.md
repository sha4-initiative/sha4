---
layout: default
title: SHA-4 Initiative
---

# SHA-4 Initiative

*Toward a standard for arithmetization-oriented hash functions.*

## The gap

The current NIST hash standards, SHA-2 and SHA-3, were designed for general-purpose computing and rely heavily on bitwise operations that do not translate efficiently into arithmetic circuits. Zero-knowledge proof systems, verifiable computation, and the infrastructure supporting post-quantum migration increasingly depend on hash functions that can be evaluated cheaply inside such circuits. In STARK settings, there exisits a substantial performance gap between a conventional hash and an arithmetization-oriented alternative. No standardised circuit-friendly hash function currently exists.

## What this is

This is a community effort to explore whether a standardised arithmetization-oriented hash function is needed and what a process to evaluate candidates might look like. The work is intended to be open and deliberative, drawing on input from cryptographers, standards bodies, and practitioners building systems that rely on circuit-efficient hashing. It is not advocacy for any specific candidate construction.

## Status

We are drafting an initial discussion note outlining the standards gap and the considerations that would inform a candidate evaluation process.

## People

- **[Conor Deegan](https://x.com/conordeegan)**, Project Eleven
- **[Justin Drake](https://x.com/drakefjustin)**, Ethereum Foundation

## Resources

- [Discussion note](docs/discussion-note)
- Technical scoping document *(coming soon)*
- [GitHub repository](https://github.com/sha4-initiative)

### References

- [New Design Techniques for Efficient Arithmetization-Oriented Hash Functions: Anemoi Permutations and Jive Compression Mode](https://eprint.iacr.org/2022/840)
- [Poseidon: A New Hash Function for Zero-Knowledge Proof Systems](https://eprint.iacr.org/2019/458)
- [NIST Privacy-Enhancing Cryptography project](https://csrc.nist.gov/projects/pec)
- [Ethereum Foundation Poseidon Cryptanalysis Initiative](https://www.poseidon-initiative.info/)

## Contact

TBC
