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
