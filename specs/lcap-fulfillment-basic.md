# LCAP Fulfillment – Basic Circulation Profile

**Version:** 1.0.1
**Status:** Frozen

---

## 1. Scope and Purpose

This document defines the **LCAP Fulfillment – Basic Circulation Profile**.

Fulfillment – Basic specifies a minimal, explicit, and deterministic set of circulation and fulfillment actions that MAY be declared by LCAP Core–conformant servers.

This profile defines:

* standard circulation actions
* action declaration requirements
* action execution semantics
* action outcome semantics
* fulfillment initiation signaling
* explicit failure and denial behavior

This profile does **not** define:

* lending policy
* patron eligibility rules
* authentication systems
* identity models
* DRM mechanisms
* delivery formats
* licensing terms
* transport protocols
* UI flows or patron experience

Fulfillment – Basic extends **LCAP Core** and MUST be implemented in full to claim conformance to this profile.

---

## 2. Normative Language and Dependencies

The key words **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** are to be interpreted as described in RFC 2119 and RFC 8174.

An implementation claiming conformance to this profile:

* MUST be fully conformant with LCAP Core
* MUST implement all requirements in this document
* MUST NOT weaken, reinterpret, or contradict Core requirements

---

## 3. Fulfillment Principles

### 3.1 Actions as Explicit Operations

In LCAP, fulfillment is expressed only through explicit action declarations.

Actions:

* represent operations that MAY be attempted
* do not imply guarantees
* MAY fail even when declared

Actions MUST NOT be inferred from:

* availability states
* formats
* links
* prior behavior

---

### 3.2 Action Attachment Point

All fulfillment actions:

* MUST be declared at the holding level
* MUST NOT be declared at catalog, collection, item, or edition levels

Higher-level resources MUST NOT imply the presence or absence of fulfillment actions.

---

### 3.3 Fulfillment Truth Discipline

Fulfillment actions represent attempts.

Action declaration MUST NOT be interpreted as:

* success
* eligibility
* availability
* entitlement

Declared actions MAY fail.

Servers MUST represent outcomes explicitly.

Clients MUST treat action execution outcomes as authoritative.

---

### 3.4 Policy Boundaries

This profile defines fulfillment semantics.

This profile does not define:

* lending policy
* eligibility rules
* circulation limits
* loan duration
* hold queue ordering
* institutional business rules

Policy decisions remain server-controlled.

Policy outcomes MUST be communicated through explicit action outcomes rather than inferred behavior.

---

## 4. Capability Declaration

Servers implementing this profile MUST declare support via the capabilities resource.

Example:

```json
{
  "extensions": [
    "https://lcap.org/specs/fulfillment-basic/1.0.1"
  ]
}
```

The Fulfillment – Basic extension identifier MUST be present for servers claiming conformance to this profile.

Clients MUST NOT assume fulfillment behavior unless this profile is declared.

---

## 5. Standard Fulfillment Actions

This profile defines the following standard actions:

* borrow
* hold
* return
* renew
* fetch

Servers MAY support any subset of these actions.

For every declared action, all requirements defined in this specification apply.

---

### 5.1 borrow

The `borrow` action represents an attempt to initiate a loan.

Possible outcomes:

* success
* failure
* denial
* pending
* indeterminate

---

### 5.2 hold

The `hold` action represents an attempt to place a reservation or hold.

Possible outcomes:

* success
* failure
* denial
* pending
* indeterminate

---

### 5.3 return

The `return` action represents an attempt to conclude an existing loan.

Possible outcomes:

* success
* failure
* denial
* indeterminate

---

### 5.4 renew

The `renew` action represents an attempt to extend an existing loan.

Possible outcomes:

* success
* failure
* denial
* pending
* indeterminate

---

### 5.5 fetch

The `fetch` action represents an attempt to initiate access to the resource associated with a holding.

The `fetch` action:

* MUST NOT imply immediate delivery
* MAY require authentication
* MAY require authorization
* MAY redirect to external systems

Possible outcomes:

* success
* failure
* denial
* pending
* indeterminate

---

## 6. Action Declaration Requirements

### 6.1 Explicit Declaration

Each action:

* MUST be explicitly declared
* MUST have a stable identifier
* MUST be discoverable without inference

Absence of an action declaration MUST be interpreted as:

* unsupported, or
* not currently permitted

and MUST NOT be interpreted as temporary failure.

---

## 7. Action Execution Semantics

Action execution mechanisms are implementation-specific.

This profile defines the semantics of fulfillment actions, not the transport used to execute them.

Servers MAY use:

* HTTP APIs
* message queues
* internal services
* proprietary transports
* future transport mechanisms

Clients and servers MUST rely on declared action semantics rather than transport assumptions.

---

## 8. Action Outcomes

### 8.1 Required Outcome Explicitness

Every action execution MUST result in an explicit outcome.

Silent failure, ambiguous success, and implied state changes are forbidden.

---

### 8.2 Outcome Types

The following outcome types are defined:

* success
* failure
* denial
* pending
* indeterminate

---

### 8.3 Outcome Semantics

#### success

The requested action completed successfully.

#### failure

The action was processed but could not be completed due to a system or operational condition.

#### denial

The action was rejected due to policy, eligibility, authorization, or other server-controlled rules.

#### pending

The action was accepted but has not yet reached a final state.

#### indeterminate

The final state of the action cannot currently be determined.

An indeterminate outcome MUST NOT be interpreted as success, failure, denial, or pending.

---

### 8.4 Additional Information

Outcome types:

* MUST be distinguishable
* MUST NOT be overloaded with policy explanation
* MAY include descriptive messages

Descriptive messages are non-normative.

---

## 9. Fetch Access Semantics

A successful fetch action MAY provide information describing how access begins.

Access mechanisms are descriptive only.

Examples include:

* redirect
* download
* stream
* external
* unknown

Fetch MUST NOT imply:

* DRM behavior
* offline capability
* format compatibility
* accessibility characteristics

Clients MUST treat access mechanisms as opaque.

---

## 10. Relationship to Availability

Availability states and fulfillment actions are independent.

* Availability MUST NOT imply action success
* Action declaration MUST NOT imply availability
* Actions MAY fail regardless of availability state

Clients MUST treat availability and actions as separate signals.

---

## 11. Authentication and Authorization

This profile does not define authentication or identity.

If an action requires authentication:

* the server MUST signal this explicitly
* the server MAY delegate to external systems

Authentication signaling is defined by LCAP Auth Handoff.

---

## 12. Error Handling and Failure Discipline

Servers MUST:

* distinguish denial from failure
* represent indeterminate states explicitly
* avoid best-effort behavior

Example error categories include:

* not-authorized
* not-eligible
* not-available
* conflict
* internal-error

Servers MAY define additional error categories.

Clients MUST:

* rely only on explicit outcomes
* avoid inference
* treat server outcomes as authoritative

---

## 13. Conformance Requirements

An implementation claiming conformance to Fulfillment – Basic MUST:

* be LCAP Core–conformant
* declare support for this profile explicitly
* declare actions only at the holding level
* implement all declared actions fully
* return explicit outcomes for every action execution
* avoid inference, defaulting, or silent fallback

An implementation MUST NOT claim conformance if it violates any requirement in this document.

---

## 14. Non-Goals and Explicit Exclusions

This profile MUST NOT define:

* lending policy rules
* patron eligibility logic
* DRM enforcement
* delivery mechanisms
* file formats
* patron identity schemas
* UI flows
* analytics or tracking

These exclusions are intentional and normative.

---

## 15. Stability and Evolution

LCAP Fulfillment – Basic is frozen.

Future revisions:

* MUST preserve backward compatibility
* MUST NOT weaken explicit outcome semantics
* MUST NOT introduce inference
* MUST respect LCAP Core invariants

Existing action semantics MUST remain stable once published.

Additional fulfillment functionality MUST be introduced through separate profiles.

---

## End of LCAP Fulfillment – Basic Circulation Profile
