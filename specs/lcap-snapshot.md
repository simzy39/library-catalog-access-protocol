# LCAP Snapshot Profile

**Version:** 1.0.0
**Status:** Frozen

---

## 1. Scope and Purpose

This document defines the **LCAP Snapshot Profile**.

LCAP Snapshot specifies a minimal, explicit, and interoperable mechanism for declaring catalog snapshots.

This profile defines:

* snapshot capability declaration
* snapshot discovery mechanisms
* snapshot metadata
* snapshot revision identification
* snapshot classification

This profile does **not** define:

* synchronization algorithms
* delta formats
* archive formats
* replication mechanisms
* preservation policy
* storage formats

Snapshots describe catalog state.

They do not alter catalog truth.

This specification extends LCAP Core and MUST NOT weaken Core semantics.

---

## 2. Normative Language and Dependencies

The key words **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** are to be interpreted as described in RFC 2119 and RFC 8174.

An implementation claiming conformance to this profile:

* MUST be LCAP Core–conformant
* MUST follow all requirements in this document
* MUST NOT weaken, reinterpret, or contradict Core requirements

A server MAY implement this profile independently of all other extensions.

---

## 3. Snapshot Principles

### 3.1 Snapshot Representation

A snapshot represents catalog state at a particular point in time.

A snapshot is not the catalog itself.

Snapshots describe catalog state but MUST NOT redefine catalog truth.

---

### 3.2 Snapshot Truth Discipline

Snapshot declarations describe only:

* snapshot identity
* snapshot scope
* snapshot revision information
* snapshot creation information

Snapshot declarations MUST NOT imply:

* access permission
* circulation eligibility
* preservation adequacy
* publication accessibility
* publication quality

Snapshots MUST NOT weaken LCAP truth discipline.

---

### 3.3 Snapshot Authority Boundaries

Snapshots are authoritative only for the metadata explicitly declared within the snapshot profile.

Snapshots are not authoritative for:

* publication meaning
* accessibility characteristics
* compatibility characteristics
* circulation outcomes
* preservation quality

Clients MUST rely on the referenced catalog resources for authoritative catalog information.

---

## 4. Capability Declaration

Servers implementing this profile MUST declare support via the capabilities resource.

Example:

```json id="1sfnpa"
{
  "extensions": [
    "https://lcap.org/specs/snapshot/1.0.0"
  ]
}
```

The Snapshot Profile extension identifier MUST be present for servers claiming conformance to this profile.

Clients MUST NOT assume snapshot support unless this profile is declared.

---

## 5. Snapshot Discovery

Catalog resources MAY declare one or more snapshot descriptors.

Example:

```json id="lp0qyk"
{
  "snapshots": {
    "href": "/catalogs/main/snapshots"
  }
}
```

Snapshot descriptors identify how snapshots may be discovered.

Clients MUST NOT infer snapshot locations from URL conventions.

Servers MAY expose multiple snapshot descriptors.

---

## 6. Snapshot Declaration

A snapshot declaration MUST include:

| Field     | Description                 |
| --------- | --------------------------- |
| id        | Stable snapshot identifier  |
| kind      | Snapshot classification     |
| generated | Snapshot creation timestamp |

Optional fields:

| Field    | Description                  |
| -------- | ---------------------------- |
| revision | Catalog revision represented |
| href     | Snapshot retrieval location  |

Example:

```json id="itj4uh"
{
  "id": "snapshot-2026-01-17",
  "kind": "full",
  "generated": "2026-01-17T00:05:00Z",
  "revision": "2026-01-17T00:00:00Z",
  "href": "/catalogs/main/snapshots/snapshot-2026-01-17"
}
```

Snapshot identifiers MUST be stable.

Snapshot identifiers MUST NOT be reassigned.

---

## 7. Revision Semantics

If present, the `revision` field identifies the catalog revision represented by the snapshot.

The `generated` field identifies when the snapshot artifact was created.

Revision and generation time MAY differ.

Clients MUST NOT treat generation time as catalog truth.

Clients MUST NOT infer revision values when revision information is absent.

---

## 8. Snapshot Classification

Allowed `kind` values:

| Value       | Meaning                             |
| ----------- | ----------------------------------- |
| full        | Complete snapshot of declared scope |
| partial     | Partial snapshot of declared scope  |
| incremental | Snapshot related to prior state     |

Incremental snapshots MUST NOT imply:

* synchronization behavior
* delta formats
* replication semantics

Clients MUST NOT infer synchronization mechanisms from snapshot classification.

---

## 9. Relationship to Catalog State

Snapshots describe catalog state.

Snapshots MUST NOT:

* modify catalog semantics
* redefine resource identity
* alter availability semantics
* alter action semantics

Referenced resources remain authoritative.

---

## 10. Error Handling

Errors MUST be explicit and machine-readable.

Example:

```json id="yrtk5m"
{
  "error": {
    "code": "snapshot-not-found",
    "message": "Requested snapshot does not exist"
  }
}
```

Servers MAY define additional error categories.

Clients MUST NOT infer snapshot behavior from error responses.

---

## 11. Conformance Requirements

An implementation claiming conformance to the Snapshot Profile MUST:

* be LCAP Core–conformant
* declare support explicitly
* expose snapshot discovery explicitly
* provide stable snapshot identifiers
* preserve catalog truth discipline
* avoid inference and silent fallback

An implementation MUST NOT claim conformance if it violates any requirement in this document.

---

## 12. Non-Goals and Explicit Exclusions

This specification MUST NOT define:

* synchronization protocols
* replication protocols
* preservation policy
* archive formats
* storage requirements
* catalog federation
* backup procedures

These exclusions are intentional and normative.

---

## 13. Stability and Evolution

LCAP Snapshot Profile is frozen.

Future revisions:

* MUST preserve backward compatibility
* MUST NOT weaken Core semantics
* MUST NOT introduce inference
* MUST respect LCAP authority boundaries

Additional snapshot functionality MUST be introduced through separate profiles.

---

## End of LCAP Snapshot Profile
