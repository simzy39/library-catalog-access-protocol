# Library Catalog & Access Protocol (LCAP)

The **Library Catalog & Access Protocol (LCAP)** is a strict, format-agnostic protocol for exposing library catalogs and access signals with **explicit state, no inference, and long-term interoperability**.

LCAP is designed for libraries, vendors, and platforms that require deterministic catalog traversal, offline and snapshot-safe operation, and unambiguous signaling of availability, actions, and failures—without assuming publication formats, DRM systems, identity models, or UI behavior.

**Current release:** v1.0.0 (Frozen)

---

## Specifications

LCAP is defined by a small set of normative specifications. These documents are authoritative.

### Core

- **[LCAP Core](specs/lcap-core.md)**  
  Defines the core resource model, availability and state rules, action declaration mechanics, capability signaling, offline support, and truth discipline.

### Fulfillment

- **[LCAP Fulfillment – Basic Circulation Profile](specs/lcap-fulfillment-basic.md)**  
  Defines standard circulation actions (borrow, hold, return, renew, fetch) and explicit outcome semantics.

### Authentication

- **[LCAP Auth Handoff](specs/lcap-auth-handoff.md)**  
  Defines a neutral, explicit mechanism for handing off authentication and authorization to external systems.

### Conformance

- **[LCAP Conformance & Validation](specs/lcap-conformance-validation.md)**  
  Defines conformance classes, validation expectations, and prohibited non-conformant behavior.

---

## Design Principles (Non-Normative Summary)

- **Format-agnostic:** Works equally with EPUB, PDF, audiobooks, comics, DAISY, and future formats.
- **No inference:** Missing information is represented as unknown, never guessed.
- **Explicit state:** Availability, actions, failures, and denials are always explicit.
- **Layered authority:** Catalog and circulation truth are separated from publication semantics.
- **Offline-first:** Deterministic traversal and snapshot-safe by design.

---

## Non-Goals

LCAP does not define DRM, payment systems, identity schemas, recommendation engines, search ranking, UI behavior, or publication semantics. These concerns are intentionally out of scope.

---

## License

LCAP specifications and documentation are licensed under the  
Creative Commons Attribution 4.0 International License (CC BY 4.0).

See the LICENSE file for details.
