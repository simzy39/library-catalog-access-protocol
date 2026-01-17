# LCAP Auth Handoff

**Version:** 1.0.0
**Status:** Frozen

---

## 1. Scope and Purpose

This document defines **LCAP Auth Handoff**.

LCAP Auth Handoff specifies a **neutral, explicit mechanism** for transitioning from an LCAP-declared action to an **external authentication and/or authorization system**, without defining identity models, credentials, or policy logic.

Auth Handoff exists to support real-world access control while preserving LCAP’s core principles:

* explicit state
* no inference
* strict authority boundaries

This specification extends **LCAP Core** and applies to fulfillment actions defined in **LCAP Fulfillment – Basic**.

---

## 2. Normative Language and Dependencies

The key words **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** are to be interpreted as described in RFC 2119 and RFC 8174.

An implementation claiming conformance to **LCAP Auth Handoff**:

* MUST be LCAP Core–conformant
* MUST follow all requirements in this document
* MUST NOT weaken or reinterpret Core or Fulfillment requirements

---

## 3. Design Principles

### 3.1 Separation of Responsibility

LCAP Auth Handoff:

* declares **that** authentication or authorization is required
* defines **how** a client is handed off

It does **not** define:

* user identity models
* credentials
* authentication protocols
* authorization policy
* session handling
* entitlement logic

Those concerns are owned by external systems.

---

### 3.2 Explicitness

Authentication requirements MUST be declared explicitly.

Clients MUST NOT infer authentication needs from:

* HTTP status codes alone
* redirects
* cookies
* format types
* prior behavior

---

## 4. Auth Handoff Model

### 4.1 Auth-Required Actions

An action MAY require authentication or authorization.

If so, the server MUST:

* declare this requirement explicitly
* provide a handoff mechanism

The absence of an auth requirement declaration MUST be interpreted as:

* no authentication is required for that action
* not as “authentication may still be required”

---

### 4.2 Handoff Declaration

When authentication is required, the server MUST provide an **auth handoff descriptor** as part of the action declaration or response.

The handoff descriptor MUST:

* identify the external system
* specify the handoff type
* provide the necessary initiation data

---

## 5. Handoff Types

This specification defines the following handoff types.

Servers MAY support one or more handoff types.

---

### 5.1 Redirect Handoff

A **redirect handoff** instructs the client to navigate the user to an external system.

A redirect handoff MUST:

* provide a target URI
* specify whether return to the LCAP server is expected

The external system is responsible for:

* authentication
* authorization
* user interaction

LCAP makes no assumptions about:

* session continuity
* credential form
* user experience

---

### 5.2 Token Exchange Handoff

A **token exchange handoff** instructs the client to obtain or present a token issued by an external system.

A token exchange handoff MUST:

* identify the required token type
* specify where the token is obtained or presented

Token semantics are **out of scope**.

---

### 5.3 Delegated Confirmation Handoff

A **delegated confirmation handoff** represents an external decision point.

In this model:

* the client initiates a handoff
* the final action outcome is determined externally
* the server later reports the outcome explicitly

This handoff type is commonly used for:

* consortia
* inter-library systems
* third-party vendors

---

## 6. Action Flow with Auth Handoff

### 6.1 Attempt Semantics

When a client attempts an action requiring authentication:

1. The server MUST respond with:

   * an explicit auth-required state
   * a handoff descriptor
2. The client MUST initiate the handoff explicitly
3. The server MUST later return an explicit action outcome

The server MUST NOT assume:

* the client completed the handoff
* authentication succeeded
* authorization was granted

---

### 6.2 Outcome Reporting

After handoff completion, the server MUST return one of the standard fulfillment outcomes:

* success
* failure
* denial
* pending

Redirect loops, silent success, or implicit completion are forbidden.

---

## 7. Failure and Denial Semantics

Authentication-related failure MUST be explicit.

Servers MUST distinguish between:

* authentication failure
* authorization denial
* operational failure

Clients MUST NOT attempt retries unless explicitly instructed.

---

## 8. Relationship to Capabilities

Servers supporting Auth Handoff MUST declare this capability explicitly.

Capabilities describe:

* server support for auth handoff
* supported handoff types

Capabilities MUST NOT:

* describe identity models
* imply authentication success
* encode policy rules

---

## 9. Security Considerations

LCAP Auth Handoff:

* does not define secure transport requirements
* does not define token formats
* does not define credential handling

Servers and clients MUST rely on external systems to ensure:

* confidentiality
* integrity
* compliance with applicable security standards

---

## 10. Conformance Requirements

An implementation claiming conformance to **LCAP Auth Handoff** MUST:

* be LCAP Core–conformant
* declare authentication requirements explicitly
* provide a valid handoff descriptor
* support explicit outcome reporting
* avoid inference and silent fallback

An implementation MUST NOT claim conformance if it:

* infers authentication needs
* relies on undocumented redirects
* hides authentication failure

---

## 11. Non-Goals and Explicit Exclusions

This specification MUST NOT define:

* identity schemas
* authentication protocols
* authorization policy
* account management
* session state models
* UI or UX behavior

These exclusions are intentional and normative.

---

## 12. Stability and Evolution

LCAP Auth Handoff is frozen.

Future revisions:

* MUST preserve backward compatibility
* MUST NOT introduce inference
* MUST respect LCAP Core authority boundaries

Additional authentication mechanisms MUST be introduced through separate specifications.

---

## End of LCAP Auth Handoff Specification

---
