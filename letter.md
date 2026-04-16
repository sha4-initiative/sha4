---
layout: default
title: Letter
permalink: /letter/
---

# An open letter on the standardisation of arithmetisation-oriented hash functions

*Published 16 April 2026*

The undersigned urge the National Institute of Standards and Technology, in coordination with the cryptographic research community and open standards bodies, to begin a pre-competition phase toward standardising an arithmetisation-oriented (AO) hash function.

The current NIST hash standards - SHA-2, SHA-3, and Ascon - were designed for conventional hardware. Arithmetisation-oriented hash functions are designed for efficient evaluation inside arithmetic circuits, where they are roughly two orders of magnitude cheaper than the standard alternatives on common zero-knowledge workloads. AO hashes are already widely deployed across proof systems, identity protocols, storage integrity schemes, and zkVMs, but no standard exists.

Without one, deployments diverge on fields, widths, linear layers, round constants, and padding rules. [EIP-5988](https://eips.ethereum.org/EIPS/eip-5988) documents how parameter divergence across Poseidon deployments obstructs a single Ethereum precompile. The Mina project found a [padding-related hash collision](https://github.com/o1-labs/o1js/issues/1428) in their own implementation.

The situation is analogous to the one that motivated NIST's lightweight cryptography effort, which produced Ascon ([SP 800-232](https://csrc.nist.gov/pubs/sp/800/232/final)). Existing standards were not broken; they were designed for a different computational target. AO hashing is in the same position today, with one additional factor: post-quantum migration. PQ signature schemes (ML-DSA, SLH-DSA) do not aggregate as cleanly as their classical predecessors, and PQ SNARKs offer a practical path to aggregation and compression. Because SNARK cost is dominated by hash evaluation, a standardised circuit-efficient hash is a prerequisite for deployable PQ-compatible ZK infrastructure.

NIST's recent standardisation processes (SHA-3, lightweight cryptography, PQC) have each taken 10 to 12 years from first engagement to final standard. Starting a pre-competition phase now would produce a standard no earlier than the mid-2030s, by which point PQ migration will already be well under way.

The cryptanalytic record for AO designs is still developing. Recent results such as the [FreeLunch](https://eprint.iacr.org/2024/347) attacks on Anemoi and Griffin show that security margins are not settled, and protocol-level techniques such as [Keccacheck](https://eprint.iacr.org/2025/1764)-style batched Keccak evaluation may narrow the performance gap in specific regimes. These considerations bear on how the process should be scoped - in particular on whether the standardisation target should be a primitive, a gadget, or both - rather than on whether to begin one.

We ask NIST and the broader community to:

1. Open a pre-competition phase that scopes requirements across target fields, arithmetisation models, and security properties.
2. Engage with existing efforts - in particular the [ZKProof](https://zkproof.org) community and the Ethereum Foundation's [Poseidon Initiative](https://www.poseidon-initiative.info/) - rather than restart their work.
3. Publish a deliberate timeline, so that implementers and standards-dependent adopters (government, enterprise, hardware) can plan around an eventual standard.

A fuller technical argument is set out in the accompanying [discussion note](/docs/discussion-note).

---

## Signatories

### Initial signatories

{% for s in site.data.signatories.initial %}- **{{ s.name }}**{% if s.affiliation %}, {{ s.affiliation }}{% endif %}{% if s.link %} · [profile]({{ s.link }}){% endif %}
{% endfor %}

### Individual signatories

{% if site.data.signatories.individuals.size == 0 %}*No additional individual signatories yet. [Add your name.](#how-to-sign)*
{% else %}{% for s in site.data.signatories.individuals %}- **{{ s.name }}**{% if s.affiliation %}, {{ s.affiliation }}{% endif %}{% if s.link %} · [profile]({{ s.link }}){% endif %}
{% endfor %}{% endif %}

### Organisational signatories

{% if site.data.signatories.organisations.size == 0 %}*No organisations have signed yet. [Add your name.](#how-to-sign)*
{% else %}{% for o in site.data.signatories.organisations %}- **{{ o.name }}** - signed by {{ o.contact }}{% if o.link %} · [site]({{ o.link }}){% endif %}
{% endfor %}{% endif %}

---

## How to sign

**Individuals** can sign by opening a pull request to [_data/signatories.yml](https://github.com/sha4-initiative/sha4/blob/main/_data/signatories.yml), or by emailing [want@sha4.info](mailto:want@sha4.info).

**Organisations** sign by email only. Write to [want@sha4.info](mailto:want@sha4.info) from an address on the organisation's own domain.

See [SIGNING.md](https://github.com/sha4-initiative/sha4/blob/main/SIGNING.md) for the entry format and review process.
