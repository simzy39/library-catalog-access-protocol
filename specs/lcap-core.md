# Library Catalog & Access Protocol (LCAP) — Core

**Version:** 1.0.0
**Status:** Frozen

---

## 1. Scope and Purpose

This document defines the **LCAP Core Protocol**.

LCAP Core specifies a format-agnostic, explicit, and deterministic protocol for exposing library catalogs and access signaling. It defines the **minimum required model and rules** for representing catalog structure, resource relationships, availability states, declared actions, server capabilities, and failure conditions.

LCAP Core does **not** define:

* circulation workflows
* authentication or identity systems
* DRM or content protection
* payment or licensing models
* search semantics
* user interface behavior
* publication semantics or meaning
* accessibility interpretation

Those concerns are explicitly out of scope and may be addressed by separate specifications.

Companion specifications MAY extend LCAP Core but MUST NOT redefine or weaken its requirements.

---

## 2. Normative Language and Conformance

The key words **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** in this document are to be interpreted as described in RFC 2119 and RFC 8174.

An **LCAP Core–conformant server** is an implementation that satisfies all requirements defined in this document and does not claim support for features it does not implement.

Partial implementations are permitted, provided all unsupported information and behavior are represented explicitly as unknown or absent.

---

## 3. Architectural Overview

LCAP defines a **hierarchical resource model** with explicit authority boundaries.

### 3.1 Resource Hierarchy

The LCAP Core resource hierarchy is:

* **Catalog**
* **Collection**
* **Item**
* **Edition**
* **Holding**

Each resource level has a distinct purpose and MUST NOT be collapsed or inferred from another level.

### 3.2 Resources vs Actions

LCAP distinguishes between:

* **Resources**, which describe catalog entities and their states
* **Actions**, which represent operations that MAY be attempted

Actions are **not links** and MUST be declared explicitly.

### 3.3 Server and Client Roles

* Servers are authoritative for the resources and states they expose.
* Clients MUST NOT infer behavior beyond what is explicitly declared.
* Clients MUST treat missing information as unknown.

---

## 4. Core Resource Types

### 4.1 Catalog

A **catalog** represents the root of an LCAP deployment.

A catalog MUST:

* have a stable identifier
* expose one or more collections
* declare server capabilities
* expose a revision identifier suitable for caching and snapshotting

A catalog MUST NOT:

* imply availability
* imply access rights
* define UI behavior

---

### 4.2 Collection

A **collection** represents a structural grouping of items.

Collections are purely organizational.

A collection MUST:

* reference items explicitly

A collection MUST NOT:

* imply availability
* imply circulation eligibility
* alter item semantics

---

### 4.3 Item

An **item** represents a conceptual work or intellectual entity.

An item:

* groups one or more editions
* has no inherent availability
* has no access semantics

An item MUST NOT:

* declare availability
* declare actions
* imply format behavior

---

### 4.4 Edition

An **edition** represents a specific manifestation of an item.

An edition MAY:

* declare descriptive format information
* reference one or more holdings

Format information is **descriptive only**.

Clients MUST NOT assume behavior, compatibility, or accessibility based solely on format.

An edition MUST NOT:

* declare availability
* declare actions
* collapse holdings

---

### 4.5 Holding

A **holding** represents a specific, actionable instance of an edition.

Holdings are the **only level** at which availability and actions may be declared.

A holding MUST:

* declare its availability state
* declare supported actions explicitly (if any)

A holding MAY:

* represent physical or digital instances
* represent pooled or singular resources

---

## 5. Availability and State Model

Availability states describe **observed or known catalog state**, not guarantees.

### 5.1 Availability States

LCAP Core defines the following availability states:

* `available`
* `unavailable`
* `restricted`
* `unknown`

The `unknown` state MUST be used when availability cannot be determined explicitly.

### 5.2 Semantics

Availability states:

* MUST be descriptive only
* MUST NOT be interpreted as guarantees of successful action execution
* MUST NOT encode policy rules

Absence of availability information MUST NOT be interpreted as `unavailable`.

---

## 6. Action Declaration

Actions represent operations that MAY be attempted.

Actions:

* MUST be declared explicitly
* MUST NOT be inferred from links, formats, or availability
* MAY fail even when declared

LCAP Core defines only the **mechanism** for declaring actions, not their semantics.

Action execution outcomes MUST be explicit:

* success
* failure
* denial
* indeterminate

Silent failure is forbidden.

---

## 7. Capability Declaration

Servers MUST declare their capabilities explicitly.

Capabilities describe:

* server behavior
* supported protocol features

Capabilities MUST NOT:

* describe publication behavior
* imply client guarantees
* override explicit state

Clients MUST rely on declared capabilities rather than assumption.

---

## 8. Offline Operation and Snapshots

LCAP Core MUST support deterministic traversal.

Servers MUST:

* provide stable identifiers
* provide revision identifiers
* ensure consistent traversal within a revision

Clients MUST be able to:

* cache responses
* consume snapshot catalogs
* operate without continuous connectivity

---

## 9. Error, Failure, and Indeterminacy

All failures MUST be explicit.

Servers MUST:

* return explicit error states
* distinguish between denial and failure
* represent indeterminate states explicitly

Best-effort behavior, silent fallback, or inferred recovery is forbidden.

---

## 10. Conformance Requirements

An LCAP Core–conformant server MUST:

* implement the full resource hierarchy
* declare availability only at the holding level
* avoid inference of any kind
* represent unknown information explicitly
* declare actions explicitly or not at all
* declare capabilities honestly
* support deterministic traversal

An implementation MUST NOT claim conformance if it violates any requirement in this document.

---

## 11. Non-Goals and Explicit Exclusions

LCAP Core MUST NOT define or require:

* DRM systems
* payment models
* licensing enforcement
* identity schemas
* authentication mechanisms
* search semantics
* recommendation systems
* accessibility interpretation
* UI or presentation rules
* publication meaning or semantics

These exclusions are intentional and normative.

---

## 12. Stability and Evolution

LCAP Core is frozen.

Future revisions:

* MUST preserve backward compatibility
* MUST NOT weaken truth discipline
* MUST NOT introduce inference
* MUST respect established authority boundaries

New functionality MUST be introduced through companion specifications.

---

## End of LCAP Core Specification

---
