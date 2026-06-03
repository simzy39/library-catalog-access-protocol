# Library Catalog & Access Protocol (LCAP)

The **Library Catalog & Access Protocol (LCAP)** is a strict, format-agnostic protocol for exposing library catalogs, availability signals, and access actions with **explicit state, zero inference, and long-term interoperability**.

LCAP is designed for **libraries, archives, repositories, vendors, and platform operators** that require deterministic catalog traversal, offline and snapshot-safe operation, and unambiguous signaling of availability, actions, and failures—without assuming publication formats, DRM systems, identity models, business rules, or UI behavior.

LCAP prioritizes custody, circulation, interoperability, and auditability over convenience or optimization. It is intended for systems that must remain trustworthy across time, vendors, and policy regimes.

**Current release:** **v1.0.0 (Frozen)**

---

## Project Status

LCAP 1.x is considered **specification-complete**.

Current work is focused on **implementation, validation, interoperability, and real-world deployment experience** rather than expansion of the specification corpus.

The immediate goal is to prove the protocol through working software and practical deployments.

---

## Specifications

LCAP is defined by a small set of normative specifications. These documents are authoritative and collectively define the protocol.

### Core

* **[LCAP Core](specs/lcap-core.md)**
  Defines the core resource model, explicit availability and state rules, action declaration mechanics, capability signaling, offline operation, identity rules, and truth discipline.

### Fulfillment

* **[LCAP Fulfillment — Basic Circulation Profile](specs/lcap-fulfillment-basic.md)**
  Defines standard circulation actions (borrow, hold, return, renew, fetch) and their explicit, non-inferential outcome semantics.

### Authentication

* **[LCAP Auth Handoff](specs/lcap-auth-handoff.md)**
  Defines a neutral, explicit mechanism for handing off authentication and authorization to external systems without embedding identity or policy assumptions.

### Search

* **[LCAP Search Profile](specs/lcap-search-profile.md)**
  Defines explicit search capability discovery, search execution, and search result semantics.

### Snapshots

* **[LCAP Snapshot Profile](specs/lcap-snapshot-profile.md)**
  Defines a minimal, interoperable mechanism for declaring catalog snapshots and snapshot metadata.

### Conformance

* **[LCAP Conformance & Validation](specs/lcap-conformance-validation.md)**
  Defines conformance classes, validation expectations, and prohibited non-conformant behavior.

---

## Roadmap

LCAP is now focused on implementation and interoperability.

### Phase 1 — Core Tooling

#### LCAPCheck

Reference validator for LCAP implementations.

Goals:

* Validate LCAP Core conformance
* Validate companion profiles
* Produce deterministic validation reports
* Serve as the reference validation implementation

#### LCAP Reference Server

Reference implementation of an LCAP server.

Goals:

* Demonstrate protocol usage
* Provide implementation guidance
* Support interoperability testing
* Serve as an educational reference

### Phase 2 — Interoperability

#### OPDS → LCAP Gateway

Translation layer enabling existing OPDS catalogs to be exposed as LCAP.

Goals:

* Lower adoption barriers
* Enable immediate experimentation
* Support coexistence with existing ecosystems
* Demonstrate practical interoperability

#### Interoperability Demonstration

Public demonstration environment showcasing:

* Catalog traversal
* Search
* Availability
* Fulfillment workflows
* Cross-system interoperability

### Phase 3 — Real-World Validation

#### Pilot Implementations

Work with libraries, repositories, archives, and platform operators to:

* Validate protocol assumptions
* Identify implementation challenges
* Improve documentation
* Refine tooling

### Phase 4 — Operational Services

Following successful implementation experience and ecosystem feedback, additional hosted services may be explored, including:

* Hosted validation
* Managed gateways
* Interoperability testing services
* Ecosystem support tooling

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
  Missing or unknown information is represented explicitly, never guessed or synthesized.

* **Explicit state**
  Availability, actions, denials, and failures are always declared, never implied.

* **Layered authority**
  Catalog and circulation truth are kept separate from publication semantics, rendering behavior, and policy decisions.

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
* Recommendation engines or ranking algorithms
* Search heuristics or relevance scoring
* UI behavior or presentation
* Publication semantics or compatibility evaluation

These concerns are out of scope by design.

---

## License

LCAP specifications and documentation are licensed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**.

See the `LICENSE` file for details.

Copyright © 2026 Heath Luke Sims.
