---
layout: default
title: Discussion note
---

# Should there be a standard arithmetisation-oriented (AO) hash function?

Authors:
- *Conor Deegan*
- *Justin Drake*

*Last updated: 14 April 2026*

NIST's hash function standards (SHA-2, SHA-3, Ascon) were designed for conventional hardware. Arithmetisation-optimised (AO) hash functions, sometimes known as SNARK-friendly or ZK-friendly hash functions, are designed for efficient evaluation inside arithmetic circuits, where they are roughly two orders of magnitude cheaper than standard alternatives for common workloads. AO hashes are already widely deployed across proof system infrastructure, identity protocols, and storage integrity systems, but no standard exists. We think a NIST standardisation process is worth beginning. This note lays out the reasoning and the open questions.

## What a standard would provide

A standard would fix parameter sets (or define a parameterisation framework), provide test vectors, and give implementers a specification to target. None of these things exist today. Implementations of the same algorithm use different fields, widths, linear mixing matrices, round constants, and output truncations. [EIP-5988](https://eips.ethereum.org/EIPS/eip-5988) notes that parameter divergence across Poseidon deployments makes it difficult to define a single Ethereum precompile. The Mina community found a [padding-related hash collision](https://github.com/o1-labs/o1js/issues/1428) in their implementation. A community specification through [ZKProof.org](https://zkproof.org) could address interoperability and test vectors. What it cannot provide is the cryptanalytic depth of a NIST competition (the SHA-3 process concentrated roughly four years of focused cryptanalysis on the candidate field and eventual winner Keccak, between the submission deadline in late 2008 and the selection in October 2012), the regulatory acceptance that government and enterprise adopters require, or the hardware support (for example in secure elements and hardware wallets) that tends to follow a NIST standard.

## Why now

When NIST began the lightweight cryptography process that produced the Ascon standard ([SP 800-232](https://csrc.nist.gov/pubs/sp/800/232/final)), the motivation was a performance gap: existing standards were too expensive for constrained devices, not because they were broken but because they were designed for different hardware. The situation with arithmetic circuits is analogous. Existing hash standards are too expensive for this computational model, and the gap is large enough that practitioners have adopted unstandardised alternatives.

ZK proof systems are seeing adoption across identity verification, storage integrity, verifiable computation, transaction processing, PQ signatures, and zkVMs. All of these use cases need circuit-efficient hashing, and in practice that means AO hash functions. Crypto infrastructure is already deploying them at scale with fragmented parameter sets and no shared specification. As adoption broadens into government and enterprise contexts, the same dependency on unevaluated primitives will apply. The Ethereum Foundation's [Poseidon Initiative](https://www.poseidon-initiative.info/) illustrates the risk: cryptanalysis produced during the programme's bounty phase prompted a reassessment of hash function choice for lean consensus, with Poseidon2 ruled out and the Foundation reverting to the original Poseidon construction.

Post-quantum migration reinforces this. PQ signature schemes (ML-DSA, SLH-DSA) produce larger signatures and are slower to verify than their classical predecessors. Native aggregation techniques that worked for classical schemes like BLS do not carry over cleanly to lattice-based or hash-based constructions. PQ SNARKs offer a practical path to PQ signature aggregation and compression. With traditional hash functions like SHA-2 and SHA-3, hash evaluations will typically dominate the cost inside these systems, which makes a standardised circuit-efficient hash function a prerequisite for PQ-compatible ZK infrastructure.

NIST's recent standardisation processes (SHA-3, lightweight cryptography, PQC) have each taken 10 to 12 years from initial engagement to final standard ([NIST IR 8114](https://csrc.nist.gov/pubs/ir/8114/final); [FIPS 202](https://csrc.nist.gov/pubs/fips/202/final); [NIST IR 8545](https://csrc.nist.gov/pubs/ir/8545/final)). In each case, NIST started before the need was fully realised: the PQ effort began before any deployed system was broken by a quantum computer, and the lightweight effort began before constrained-device deployment reached its current scale. Even by that precedent, starting a pre-competition phase now would produce a standard no earlier than the mid-2030s, by which point PQ migration will already be well under way. NIST has already engaged with ZK proof technology through its Privacy-Enhancing Cryptography project ([NIST CSRC PEC/ZKP project page](https://csrc.nist.gov/projects/pec/zkproof)), and ZK-friendly primitive standardisation has been raised at NIST workshops including WPEC 2024 ([NIST CSRC WPEC 2024 proceedings](https://csrc.nist.gov/Events/2024/wpec2024)).

## Close

The cryptanalytic record for AO designs is still developing, with active work on algebraic attacks and reduced-round behaviour, and recent results such as the [FreeLunch](https://eprint.iacr.org/2024/347) attacks on Anemoi and Griffin show that margins are not yet settled. Protocol-level techniques for proving standard hashes efficiently (for example [Keccacheck](https://eprint.iacr.org/2025/1764)-style batched Keccak evaluation) may also narrow the gap in some regimes, which raises the legitimate question of whether the standards target should be a primitive or a gadget. Open questions remain around whether the candidate landscape is mature enough, how to standardise across target fields and arithmetisation models, what security properties to require, and whether a traditional competition is the right process for a design space this parameterised. We are circulating this to cryptographers, hash function designers, proof system engineers, and standards practitioners, and we would welcome responses on any aspect of the above, and on what we have missed.

This document and supporting research are available at [sha4.info](https://sha4.info). Discussion, corrections, and dissenting views are welcome as issues on the GitHub repository at [https://github.com/sha4-initiative/sha4/issues](https://github.com/sha4-initiative/sha4/issues). You can also reach us directly at sha4-info at protonmail.com.
