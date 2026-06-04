# LCAP Conformance & Validation

**Version:** 1.0.0
**Status:** Frozen

---

## 1. Scope and Purpose

This document defines the **LCAP Conformance & Validation Specification**.

This specification defines:

* LCAP conformance classes
* validation requirements
* machine-checkable constraints
* testability requirements
* rules for conformance claims

Its purpose is to ensure that a claim of:

> "LCAP-conformant"

is precise, verifiable, and meaningful.

This specification does **not**:

* define new protocol behavior
* extend LCAP Core semantics
* modify companion profile semantics
* define UI requirements
* define operational requirements
* define certification programs

This specification establishes how conformance is evaluated, not how protocol behavior works.

---

## 2. Normative Language and Dependencies

The key words **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** are to be interpreted as described in RFC 2119 and RFC 8174.

An implementation claiming conformance:

* MUST satisfy all requirements of every claimed conformance class
* MUST NOT claim conformance to unsupported classes
* MUST NOT weaken or reinterpret protocol requirements

---

## 3. Relationship to Specifications

This specification defines conformance requirements for:

* LCAP Core
* LCAP Fulfillment – Basic
* LCAP Auth Handoff
* LCAP Search
* LCAP Snapshot

This specification derives authority from those specifications.

It does not replace, reinterpret, or supersede their normative requirements.

---

## 4. Conformance Principles

### 4.1 Profile-Scoped Conformance

LCAP conformance is profile-scoped and additive.

An implementation:

* MUST claim at least one conformance class
* MUST satisfy all requirements of each claimed class
* MUST NOT claim conformance to a class it does not fully satisfy

Conformance classes are orthogonal and non-exclusive.

---

### 4.2 Companion Profile Independence

Companion profiles are independently claimable.

Conformance to one companion profile MUST NOT imply conformance to another companion profile.

Support for a companion profile MUST be declared explicitly.

---

### 4.3 Truthful Conformance Claims

A conformance claim is itself protocol metadata.

Conformance claims MUST be truthful.

Implementations MUST NOT:

* overstate support
* imply support for undeclared features
* claim partial support as full conformance
* rely on ambiguous terminology

Conformance claims MUST be auditable.

---

### 4.4 Validation Truth Discipline

Validation results MUST reflect observed behavior.

Validators MUST NOT infer compliance from absent information.

Validation outcomes MUST distinguish between:

* conformant
* non-conformant
* indeterminate

Indeterminate validation results MUST NOT be interpreted as conformant or non-conformant.

Validation MUST NOT weaken LCAP truth discipline.

---

### 4.5 Testability

Conformance requirements MUST be testable.

Requirements SHOULD be:

* machine-checkable
* repeatable
* deterministic

Requirements that cannot be fully machine-checked MUST remain auditable through scenario testing.

---

### 4.6 Conformance Authority Boundaries

Conformance is authoritative only for protocol compliance.

Conformance is not authoritative for:

* implementation quality
* performance
* security
* usability
* accessibility
* business suitability

Conformance does not imply superiority, suitability, or preference.

---

## 5. Conformance Classes

### 5.1 LCAP Core–Conformant Server

A server claiming LCAP Core conformance MUST satisfy all requirements of LCAP Core.

Required characteristics:

* implements the full resource hierarchy:

  * catalog
  * collection
  * item
  * edition
  * holding
* declares availability only at the holding level
* preserves truth discipline
* avoids inference
* separates resources and actions
* declares capabilities explicitly
* supports deterministic traversal

A Core-conformant server:

* MAY omit Fulfillment
* MAY omit Auth Handoff
* MAY omit Search
* MAY omit Snapshot
* MAY expose read-only catalogs

---

### 5.2 LCAP Fulfillment – Basic Conformant Server

A server claiming Fulfillment conformance MUST:

* be LCAP Core–conformant
* implement LCAP Fulfillment – Basic in full

Required characteristics:

* declares the Fulfillment extension explicitly
* declares actions only at the holding level
* implements all declared actions fully
* returns only defined outcome types:

  * success
  * failure
  * denial
  * pending
  * indeterminate
* represents failures explicitly
* allows action failure even when actions are declared

A Fulfillment-conformant server MUST NOT:

* imply DRM behavior
* imply delivery semantics
* weaken fulfillment truth discipline

---

### 5.3 LCAP Auth Handoff–Conformant Server

A server claiming Auth Handoff conformance MUST:

* be LCAP Core–conformant
* implement LCAP Auth Handoff in full

Required characteristics:

* declares the Auth Handoff extension explicitly
* declares authentication requirements explicitly
* provides valid handoff descriptors
* supports explicit authentication challenge signaling
* avoids inference of authentication requirements

---

### 5.4 LCAP Search–Conformant Server

A server claiming Search conformance MUST:

* be LCAP Core–conformant
* implement LCAP Search in full

Required characteristics:

* declares the Search extension explicitly
* exposes search discovery explicitly
* represents search results as ordinary LCAP resources
* preserves resource identity
* preserves resource semantics
* avoids inference

---

### 5.5 LCAP Snapshot–Conformant Server

A server claiming Snapshot conformance MUST:

* be LCAP Core–conformant
* implement LCAP Snapshot in full

Required characteristics:

* declares the Snapshot extension explicitly
* exposes snapshot discovery explicitly
* provides stable snapshot identifiers
* preserves catalog truth discipline
* avoids inference

---

### 5.6 Read-Only LCAP Catalog

A server MAY claim Read-Only LCAP conformance if:

* it is LCAP Core–conformant
* it declares no actions
* it declares no Fulfillment capability

Read-only status is a conformance class, not a limitation.

Read-only implementations remain fully conformant Core implementations.

This class exists to support:

* national libraries
* preservation catalogs
* archival mirrors
* discovery-only deployments

---

## 6. Capability Claim Rules

All conformance claims MUST be supported by the capabilities resource.

A conformant capabilities resource MUST:

* declare supported features truthfully
* list all supported extensions explicitly
* omit unsupported capabilities

A server MUST NOT:

* imply support for undeclared features
* rely on defaults or assumptions
* overload capability meanings

---

## 7. Validation Surfaces

### 7.1 Structural Validation

Verifies:

* syntactic correctness
* required fields
* forbidden fields
* schema compliance

This surface is machine-checkable.

### 7.2 Semantic Validation

Verifies:

* resource hierarchy rules
* availability placement
* action placement
* capability declarations
* truth discipline requirements

This surface is partially machine-checkable.

### 7.3 Behavioral Validation

Verifies:

* action execution semantics
* explicit outcomes
* authentication signaling
* search behavior consistency
* snapshot behavior consistency

This surface requires scenario testing.

### 7.4 Claim Validation

Verifies:

* conformance claims
* extension declarations
* implementation behavior

This surface is auditable.

---

## 8. Machine-Checkable Validation

Implementations SHOULD be validated using:

* JSON Schemas
* schema collections
* deterministic test suites

Validation artifacts derive authority from the protocol specifications.

Validation artifacts SHOULD:

* enforce required fields
* enforce structural constraints
* prohibit implicit state where applicable

Validation artifacts MUST NOT:

* encode policy logic
* encode UI assumptions
* encode publication semantics

---

## 9. Test Suite Expectations

A conformant implementation MUST be testable using:

* deterministic requests
* repeatable traversal
* predictable signaling
* auditable outcomes

A valid test suite SHOULD include:

* positive conformance cases
* negative conformance cases
* truth discipline checks
* capability declaration checks
* action outcome checks
* authentication signaling checks
* search validation checks
* snapshot validation checks

---

## 10. Conformance Claims

Implementations MUST express conformance claims using exact class names and explicit version numbers.

Examples:

* LCAP Core 1.0.0–Conformant Server
* LCAP Fulfillment – Basic 1.0.1–Conformant Server
* LCAP Search 1.0.0–Conformant Server

Claims MUST include:

* protocol version
* conformance class
* supported extensions

Claims MUST correspond to actual deployed behavior.

Conformance classes are version-specific.

Conformance to one version MUST NOT imply conformance to another version.

Claims MUST NOT be:

* vague
* approximate
* implied

---

## 11. Non-Goals and Explicit Exclusions

This specification MUST NOT define:

* certification programs
* trademarks
* branding requirements
* procurement rules
* implementation licensing
* runtime performance guarantees

These exclusions are intentional and normative.

---

## 12. Stability and Evolution

LCAP Conformance & Validation is frozen.

Future revisions:

* MAY add new conformance classes
* MUST preserve backward compatibility
* MUST NOT weaken existing conformance classes
* MUST NOT weaken protocol semantics

Additional validation functionality MUST be introduced through separate specifications.

---

## End of LCAP Conformance & Validation Specification
