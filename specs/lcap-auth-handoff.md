# LCAP Auth Handoff

**Version:** 1.0.0
**Status:** Frozen

---

## 1. Scope and Purpose

This document defines **LCAP Auth Handoff**.

LCAP Auth Handoff specifies a neutral, explicit mechanism for transitioning from an LCAP-declared action to an external authentication and/or authorization system.

Auth Handoff exists to support real-world access control while preserving LCAP Core principles:

* explicit state
* no inference
* truth discipline
* authority boundaries

This specification defines:

* authentication requirement signaling
* authentication challenge signaling
* authentication handoff descriptors
* post-authentication action resumption

This specification does **not** define:

* identity models
* credentials
* authentication protocols
* authorization policy
* entitlement rules
* patron schemas
* session models
* UI behavior

Those concerns remain external.

This specification extends LCAP Core and MAY be used by Fulfillment profiles.

---

## 2. Normative Language and Dependencies

The key words **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** are to be interpreted as described in RFC 2119 and RFC 8174.

An implementation claiming conformance to this specification:

* MUST be LCAP Core–conformant
* MUST follow all requirements in this document
* MUST NOT weaken or reinterpret Core requirements

---

## 3. Design Principles

### 3.1 Separation of Responsibility

LCAP Auth Handoff:

* declares that authentication or authorization is required
* defines how a client is handed off

It does not define:

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

Clients MUST NOT infer authentication requirements from:

* redirects
* cookies
* status codes alone
* format declarations
* prior behavior

---

### 3.3 Authentication State Discipline

Authentication requirements are explicit state.

Authentication requirement declaration MUST NOT be interpreted as:

* authentication success
* authorization success
* entitlement
* action success

Authentication outcomes and action outcomes remain separate.

Clients MUST treat authentication state and action outcomes as independent signals.

---

## 4. Capability Declaration

Servers implementing this specification MUST declare support via the capabilities resource.

Example:

```json
{
  "extensions": [
    "https://lcap.org/specs/auth-handoff/1.0.0"
  ]
}
```

The Auth Handoff extension identifier MUST be present for servers claiming conformance to this specification.

Clients MUST NOT assume authentication handoff behavior unless this extension is declared.

---

## 5. Authentication Requirement Signaling

Actions that require authentication MUST declare:

```json
{
  "auth_required": true
}
```

Rules:

* `auth_required: true` indicates authentication is required before or during action execution
* absence of `auth_required` MUST be interpreted as false
* clients MUST NOT infer authentication requirements from action failure

---

## 6. Authentication Challenge Response

If an unauthenticated client attempts an authenticated action, the server MUST return an explicit authentication challenge.

Example:

```json
{
  "error": {
    "code": "not-authorized",
    "message": "Authentication required",
    "auth": {
      "type": "redirect",
      "href": "https://auth.example/login",
      "return_to": "https://lcap.example/actions/borrow"
    }
  }
}
```

---

## 7. Auth Handoff Descriptor

The `auth` object describes how authentication begins.

Required fields:

| Field | Description                |
| ----- | -------------------------- |
| type  | Handoff mechanism          |
| href  | Authentication entry point |

Optional fields:

| Field     | Description     |
| --------- | --------------- |
| return_to | Resume location |
| state     | Opaque state    |

---

## 8. Supported Handoff Types

Allowed values:

| Type     | Meaning                                           |
| -------- | ------------------------------------------------- |
| redirect | Client redirects user                             |
| external | External system handles interaction               |
| unknown  | Authentication required but mechanism unspecified |

Rules:

* clients MUST treat handoff mechanisms as opaque
* servers MUST NOT imply specific authentication technologies
* handoff types describe client behavior, not authentication architecture

---

## 9. Post-Authentication Resumption

After successful authentication:

* clients MAY retry the original action
* servers MUST NOT assume successful authentication until verified
* action execution MUST remain explicit and failure-capable

Authentication success MUST NOT imply:

* authorization success
* entitlement
* action success

---

## 10. State Management

Servers MAY:

* maintain server-side state
* use opaque tokens
* use cookies
* use sessions

Clients MUST NOT depend on any specific state model.

---

## 11. Error Handling

Authentication-related failures MUST be explicit.

Example:

```json
{
  "error": {
    "code": "authentication-failed",
    "message": "Login unsuccessful"
  }
}
```

Authentication failure MUST remain distinguishable from:

* authorization denial
* eligibility failure
* availability failure
* operational failure

Authentication state MAY be indeterminate.

An indeterminate authentication state MUST NOT be interpreted as:

* success
* failure
* authorization
* denial

Servers MUST represent indeterminate authentication states explicitly when known.

---

## 12. Security Considerations

This specification intentionally avoids defining:

* credential handling
* token formats
* token storage
* cryptographic requirements

Implementers MUST follow appropriate security practices for their chosen authentication systems.

---

## 13. Conformance Requirements

An implementation claiming conformance to LCAP Auth Handoff MUST:

* declare support explicitly
* declare authentication requirements explicitly
* provide a valid handoff descriptor
* support explicit authentication challenge signaling
* avoid inference and silent fallback

An implementation MUST NOT claim conformance if it:

* infers authentication requirements
* relies on undocumented redirects
* hides authentication failure

---

## 14. Non-Goals and Explicit Exclusions

This specification MUST NOT define:

* identity schemas
* authentication protocols
* authorization policy
* account management
* patron data models
* session semantics
* UI behavior

These exclusions are intentional and normative.

---

## 15. Stability and Evolution

LCAP Auth Handoff is frozen.

Future revisions:

* MUST preserve backward compatibility
* MUST NOT introduce inference
* MUST respect LCAP Core authority boundaries

Additional authentication mechanisms MUST be introduced through separate specifications.

---

## End of LCAP Auth Handoff Specification
