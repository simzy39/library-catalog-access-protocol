# LCAP  
## Library Catalog & Access Protocol

LCAP is a strict, format-agnostic protocol for exposing library catalogs and access options **truthfully and explicitly**.

It is designed as a modern replacement for OPDS-style feeds, eliminating inference, hidden behavior, and guesswork.  
LCAP allows systems to say exactly what they know — and clearly say when they don’t.

---

## What LCAP is

- A protocol for **catalog discovery and access signaling**
- Format-agnostic (print, EPUB, PDF, audio, DAISY, comics, future formats)
- Explicit about availability, restrictions, and actions
- Safe for offline, snapshot, and preservation use
- Suitable for libraries, vendors, aggregators, consortia, and national systems

LCAP is **not** a UI framework, business model, DRM system, or identity platform.

---

## Core principles

- **No inference**  
  Missing information is represented as `unknown`, never guessed.

- **Explicit actions**  
  Operations (borrow, hold, fetch, etc.) are declared explicitly and may fail.

- **Clear authority boundaries**  
  LCAP is authoritative about catalog structure and access signaling, not publication meaning or policy enforcement.

- **Incremental adoption**  
  Discovery-only catalogs are fully conformant.

Strictness is intentional. It enables trust, interoperability, and long-term stability.

---

## The LCAP specification suite

LCAP is published as a small, modular set of specifications:

- **LCAP Core**  
  Catalog structure; items, editions, holdings; availability and restriction states; action declaration; capabilities; snapshots.

- **LCAP Fulfillment – Basic**  
  Optional circulation actions (borrow, hold, return, renew, fetch) with explicit outcomes.

- **LCAP Auth Handoff**  
  Explicit transition to external authentication/authorization systems (without defining identity).

- **LCAP Conformance & Validation**  
  Defines conformance classes and validation rules.

Each specification is independently versioned and optional unless its functionality is required.

---

## Documentation

Start here:

- **What is LCAP?**  
  Non-technical overview of intent, scope, and design philosophy.

- **LCAP Conformance Cheat Sheet**  
  One-page explanation of what compliance means — and what is forbidden.

- **Hello, LCAP**  
  Minimal, fully conformant, discovery-only example.

- **OPDS → LCAP Migration Note**  
  Practical guidance for mapping existing OPDS systems without rewrites.

---

## Status

- **LCAP Core**: Frozen and stable  
- Companion specifications evolve independently

LCAP favors correctness over convenience and explicitness over heuristics.

---

## In one sentence

> **LCAP is a strict, format-agnostic protocol that lets libraries say exactly what they know — and nothing they don’t — about their catalogs and access options.**

---

## License

LCAP specifications and documentation are licensed under the  
**Creative Commons Attribution 4.0 International License (CC BY 4.0)**.

See the LICENSE file for full terms.
