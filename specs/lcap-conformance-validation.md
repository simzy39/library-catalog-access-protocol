# LCAP Conformance & Validation

**Version:** 1.0.0
**Status:** Frozen

---

## 1. Scope and Purpose

This document defines **conformance requirements and validation rules** for the Library Catalog & Access Protocol (LCAP).

It specifies:

* conformance classes
* requirements for claiming conformance
* rules governing partial implementations
* conditions under which conformance MUST be denied
* validation expectations

This document does **not** define:

* certification authorities
* governance bodies
* approval processes
* tooling implementations

Conformance is a **self-declared, testable claim**.

---

## 2. Normative Language and Dependencies

The key words **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** are to be interpreted as described in RFC 2119 and RFC 8174.

This specification depends normatively on:

* **LCAP Core**
* **LCAP Fulfillment – Basic** (if claimed)
* **LCAP Auth Handoff** (if claimed)

---

## 3. Conformance Philosophy

LCAP conformance prioritizes:

* honesty over completeness
* explicitness over convenience
* correctness over compatibility

An implementation is **not required to implement all LCAP features**.
It *is required* to represent everything it does implement **truthfully and explicitly**.

Missing functionality is acceptable.
Inference is not.

---

## 4. Conformance Classes

LCAP defines the following conformance classes.

An implementation MAY claim any subset, provided all requirements for each claimed class are met.

---

### 4.1 LCAP Core–Conformant Server

An implementation claiming **LCAP Core conformance** MUST:

* implement the full LCAP Core resource hierarchy
* expose catalog, collection, item, edition, and holding resources
* declare availability **only at the holding level**
* represent unknown information explicitly
* avoid inference of any kind
* declare actions explicitly or not at all
* declare server capabilities honestly
* support deterministic traversal and revisioning

A Core–conformant server:

* MAY be discovery-only
* MAY declare zero actions
* MAY omit circulation and authentication

---

### 4.2 LCAP Fulfillment – Basic–Conformant Server

An implementation claiming **LCAP Fulfillment – Basic conformance** MUST:

* be LCAP Core–conformant
* implement all requirements of the Fulfillment – Basic specification
* declare fulfillment actions only at the holding level
* return explicit outcomes for every action execution
* distinguish success, failure, denial, and pending states
* avoid implied or guaranteed outcomes

Partial implementation of fulfillment actions is permitted, but **only declared actions are allowed**.

---

### 4.3 LCAP Auth Handoff–Conformant Server

An implementation claiming **LCAP Auth Handoff conformance** MUST:

* be LCAP Core–conformant
* implement all requirements of the Auth Handoff specification
* declare authentication requirements explicitly
* provide valid handoff descriptors
* return explicit post-handoff outcomes

Implicit authentication behavior is forbidden.

---

### 4.4 Read-Only LCAP Core Catalog

A **Read-Only LCAP Core Catalog** is a valid conformance class.

Such an implementation:

* MUST be LCAP Core–conformant
* MUST declare no actions
* MUST not imply access, circulation, or authentication

This class is suitable for:

* national libraries
* legal deposit systems
* preservation mirrors
* offline snapshots

---

## 5. Partial Implementations

Partial implementations are explicitly allowed.

An implementation MAY:

* omit entire feature areas
* support only discovery
* support only a subset of actions

However:

* unsupported features MUST be absent or explicitly marked as unknown
* clients MUST NOT be expected to guess or infer support

Claiming partial support for a feature while relying on inference is non-conformant.

---

## 6. Prohibited Behavior (Non-Conformance)

An implementation is **non-conformant** if it:

* infers availability at item or edition level
* treats missing information as false
* infers action eligibility
* infers authentication requirements
* uses links to imply actions
* assumes formats imply behavior or accessibility
* performs silent fallback or best-effort behavior
* claims conformance to unsupported specifications

There are **no exceptions**.

---

## 7. Validation Expectations

LCAP conformance MUST be **testable**.

Validation MAY include:

* structural validation (schemas, shapes)
* semantic validation (state placement and meaning)
* behavioral validation (explicit outcomes)
* traversal validation (determinism and revision consistency)

LCAP does **not** require any specific validation tool or authority.

---

## 8. Conformance Claims

Conformance claims MUST be explicit and precise.

Acceptable examples:

* “LCAP Core–Conformant Server”
* “LCAP Core + Fulfillment – Basic–Conformant”
* “Read-Only LCAP Core Catalog”

Unacceptable examples:

* “LCAP-compatible”
* “LCAP-inspired”
* “Mostly LCAP”
* “LCAP-like”

Ambiguous claims are forbidden.

---

## 9. Relationship to Clients

This specification governs **server conformance only**.

Clients:

* MAY implement heuristics for user experience
* MUST NOT rely on inference for protocol correctness
* MUST treat unknown information as unknown

Client behavior does not affect server conformance claims.

---

## 10. Stability and Enforcement

This conformance specification is frozen.

Future revisions:

* MUST preserve existing conformance classes
* MUST NOT weaken conformance requirements
* MAY introduce new conformance classes only through new specifications

LCAP relies on:

* public documentation
* explicit claims
* verifiable behavior

There is no central enforcement authority.

---

## End of LCAP Conformance & Validation Specification

---
