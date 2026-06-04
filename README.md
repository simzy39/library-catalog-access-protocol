# Library Catalog & Access Protocol (LCAP)

The **Library Catalog & Access Protocol (LCAP)** is a strict, format-agnostic protocol for exposing library catalogs, availability signals, access actions, search capabilities, and snapshot declarations with **explicit state, zero inference, and long-term interoperability**.

LCAP is designed for **libraries, archives, repositories, vendors, and platform operators** that require deterministic catalog traversal, offline and snapshot-safe operation, and unambiguous signaling of availability, actions, authentication requirements, and failures—without assuming publication formats, DRM systems, identity models, business rules, ranking algorithms, or UI behavior.

LCAP prioritizes **truthfulness, determinism, interoperability, custody, circulation, and auditability** over convenience or optimization. It is intended for systems that must remain trustworthy across time, vendors, and policy regimes.

**Current release:** **v1.0.0 (Frozen)**

---

## Project Status

LCAP 1.x is considered **specification-complete**.

The protocol family is currently composed of:

* LCAP Core
* LCAP Fulfillment – Basic
* LCAP Auth Handoff
* LCAP Search
* LCAP Snapshot
* LCAP Conformance & Validation

Current work is focused on:

* implementation
* validation
* interoperability
* deployment experience

rather than expansion of the specification corpus.

The immediate goal is to validate the protocol through working software and real-world deployments.

---

## Specifications

LCAP is defined by a small set of normative specifications. Together, these documents define the complete LCAP 1.x protocol family.

### Core

* **[LCAP Core](specs/lcap-core.md)**
  Defines the core resource model, truth discipline, authority boundaries, capability declaration, availability semantics, action declaration rules, and deterministic traversal requirements.

### Fulfillment

* **[LCAP Fulfillment – Basic Circulation Profile](specs/lcap-fulfillment-basic.md)**
  Defines standard circulation actions (`borrow`, `hold`, `return`, `renew`, `fetch`) and their explicit outcome semantics.

### Authentication

* **[LCAP Auth Handoff](specs/lcap-auth-handoff.md)**
  Defines explicit authentication requirement signaling and handoff to external authentication and authorization systems.

### Search

* **[LCAP Search](specs/lcap-search.md)**
  Defines explicit search discovery, search result representation, and discovery semantics.

### Snapshots

* **[LCAP Snapshot](specs/lcap-snapshot.md)**
  Defines explicit snapshot discovery, snapshot metadata, revision identification, and offline catalog state representation.

### Conformance

* **[LCAP Conformance & Validation](specs/lcap-conformance-validation.md)**
  Defines conformance classes, validation surfaces, conformance claims, and testability requirements.

---

## Roadmap

LCAP is now focused on implementation, validation, and interoperability.

### Phase 1 — Validation & Reference Tooling

#### LCAPCheck

Reference validator and conformance testing tool for LCAP implementations.

Goals:

* Validate LCAP Core conformance
* Validate companion profile conformance
* Produce deterministic validation reports
* Serve as the reference validation implementation
* Implement the LCAP Conformance & Validation specification

#### LCAP Reference Server

Reference implementation of an LCAP server.

Goals:

* Demonstrate protocol usage
* Provide implementation guidance
* Support interoperability testing
* Serve as an educational reference

---

### Phase 2 — Ecosystem Interoperability

#### OPDS → LCAP Gateway

Translation layer enabling existing OPDS catalogs to be exposed as LCAP.

Goals:

* Lower adoption barriers
* Enable immediate experimentation
* Support coexistence with existing ecosystems
* Demonstrate practical interoperability

#### Interoperability Demonstration

Public demonstration environment showcasing:

* catalog traversal
* search
* availability
* fulfillment workflows
* authentication handoff
* snapshot support
* cross-system interoperability

---

### Phase 3 — Real-World Validation

#### Pilot Implementations

Work with libraries, archives, repositories, and platform operators to:

* validate protocol assumptions
* identify implementation challenges
* improve documentation
* refine tooling
* gather interoperability feedback

---

### Phase 4 — Operational Services

Following successful implementation experience and ecosystem feedback, additional hosted services may be explored, including:

* hosted validation
* managed gateways
* interoperability testing services
* ecosystem support tooling

These services are intentionally deferred until the protocol and tooling have been validated through real-world deployments.

---

## Planned Implementations

### Official Projects

Planned:

* LCAPCheck
* LCAP Reference Server
* OPDS → LCAP Gateway

### Third-Party Implementations

None yet.

---

## Design Principles (Non-Normative Summary)

* **Format-agnostic**
  Works equally with ebooks, audiobooks, archives, repositories, and future publication forms.

* **No inference**
  Missing, unknown, or indeterminate information is represented explicitly and never guessed.

* **Explicit state**
  Availability, actions, authentication requirements, denials, failures, and outcomes are always declared, never implied.

* **Truth discipline**
  Systems communicate only what is known and authoritative.

* **Layered authority**
  Catalog truth, fulfillment semantics, authentication requirements, search discovery, and snapshot metadata remain separate concerns.

* **Offline-first**
  Deterministic traversal and snapshot-safe operation are architectural requirements, not optimizations.

* **Interoperability-first**
  The protocol exists to reduce ambiguity and integration cost across systems and vendors.

---

## Non-Goals

LCAP intentionally does not define or standardize:

* DRM systems or content protection schemes
* Payment or commerce models
* Identity schemas or authentication providers
* Authentication protocols
* Recommendation engines or ranking algorithms
* Search heuristics or relevance scoring
* Semantic search
* UI behavior or presentation
* Publication semantics or compatibility evaluation
* Preservation policy
* Synchronization or replication protocols

These concerns are intentionally out of scope.

---

## License

LCAP specifications and documentation are licensed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**.

See the `LICENSE` file for details.

Copyright © 2026 Heath Luke Sims.
