# Library Catalog & Access Protocol (LCAP)

The **Library Catalog & Access Protocol (LCAP)** is a strict, format-agnostic protocol for exposing library catalogs and access signals with **explicit state, zero inference, and long-term interoperability**.

LCAP is designed for **libraries, archives, vendors, and platforms** that require deterministic catalog traversal, offline and snapshot-safe operation, and unambiguous signaling of **availability, actions, and failures**—without assuming publication formats, DRM systems, identity models, business rules, or UI behavior.

LCAP prioritizes custody, circulation, and auditability over convenience or optimization.  
It is intended for systems that must remain trustworthy across time, vendors, and policy regimes.

**Current release:** **v1.0.0 (Frozen)**

---

## Specifications

LCAP is defined by a small set of **normative specifications**.  
These documents are authoritative and collectively define the protocol.

### Core

- **[LCAP Core](specs/lcap-core.md)**  
  Defines the core resource model, explicit availability and state rules, action declaration mechanics, capability signaling, offline operation, and truth discipline.

### Fulfillment

- **[LCAP Fulfillment — Basic Circulation Profile](specs/lcap-fulfillment-basic.md)**  
  Defines standard circulation actions (borrow, hold, return, renew, fetch) and their explicit, non-inferential outcome semantics.

### Authentication

- **[LCAP Auth Handoff](specs/lcap-auth-handoff.md)**  
  Defines a neutral, explicit mechanism for handing off authentication and authorization to external systems without embedding identity or policy assumptions.

### Conformance

- **[LCAP Conformance & Validation](specs/lcap-conformance-validation.md)**  
  Defines conformance classes, validation expectations, and prohibited non-conformant behavior.

---

## Design Principles (Non-Normative Summary)

- **Format-agnostic**  
  Works equally with EPUB, PDF, audiobooks, comics, DAISY, and future publication forms.

- **No inference**  
  Missing or unknown information is represented explicitly, never guessed or synthesized.

- **Explicit state**  
  Availability, actions, denials, and failures are always declared, never implied.

- **Layered authority**  
  Catalog and circulation truth are kept separate from publication semantics, rendering behavior, and policy decisions.

- **Offline-first**  
  Deterministic traversal and snapshot-safe operation are architectural requirements, not optimizations.

---

## Non-Goals

LCAP intentionally does **not** define or standardize:

- DRM systems or content protection schemes  
- Payment or commerce models  
- Identity schemas or authentication providers  
- Recommendation engines or ranking algorithms  
- Search heuristics or relevance scoring  
- UI behavior or presentation  
- Publication semantics or compatibility evaluation  

These concerns are out of scope by design.

---

## License

LCAP specifications and documentation are licensed under the  
**Creative Commons Attribution 4.0 International License (CC BY 4.0)**.

See the `LICENSE` file for details.
