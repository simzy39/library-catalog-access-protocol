# LCAP Search Profile

**Version:** 1.0.0
**Status:** Frozen

---

## 1. Scope and Purpose

This document defines the **LCAP Search Profile**.

LCAP Search specifies a minimal, explicit, and interoperable mechanism for catalog discovery.

This profile defines:

* search capability declaration
* search discovery mechanisms
* search expression semantics
* search result representation
* search result ordering semantics
* pagination semantics

This profile does **not** define:

* ranking algorithms
* relevance scoring
* fuzzy matching
* language processing
* recommendation systems
* semantic search
* personalization
* analytics

Search remains a discovery mechanism only.

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

## 3. Search Principles

### 3.1 Discovery Only

Search exists solely to assist resource discovery.

Search results represent discovery signals, not authoritative statements about the resources themselves.

Search MUST NOT alter:

* resource identity
* resource semantics
* availability semantics
* action semantics

---

### 3.2 Search Truth Discipline

Search results indicate only that a resource matched server-defined search criteria.

Search results MUST NOT be interpreted as:

* recommendation
* endorsement
* authority
* quality
* semantic equivalence
* relevance guarantees

Servers MUST NOT imply characteristics beyond those explicitly represented by the matching resources.

---

### 3.3 Search Authority Boundaries

Search is authoritative only for discovery.

Search is not authoritative for:

* publication meaning
* accessibility characteristics
* compatibility characteristics
* circulation outcomes
* recommendation quality
* resource importance

Clients MUST rely on the referenced resources themselves for authoritative information.

---

## 4. Capability Declaration

Servers implementing this profile MUST declare support via the capabilities resource.

Example:

```json
{
  "extensions": [
    "https://lcap.org/specs/search/1.0.0"
  ]
}
```

The Search Profile extension identifier MUST be present for servers claiming conformance to this profile.

Clients MUST NOT assume search support unless this profile is declared.

---

## 5. Search Discovery

Catalog resources MAY declare one or more search descriptors.

Example:

```json
{
  "search": {
    "href": "/search"
  }
}
```

Search descriptors identify how search may be discovered.

Clients MUST NOT infer search endpoints from URL conventions.

Servers MAY expose multiple search descriptors.

---

## 6. Search Expressions

Search expressions are implementation-defined.

Servers MAY support:

* keyword matching
* metadata matching
* full-text matching
* other matching strategies

This specification does not define:

* searchable fields
* query languages
* query syntax
* matching algorithms

Servers SHOULD document supported search behavior when search is exposed publicly.

Clients MUST NOT infer search scope beyond what is explicitly documented.

---

## 7. Search Result Representation

Search results MUST be represented as ordinary LCAP collection resources.

Example:

```json
{
  "type": "collection",
  "id": "search-results",
  "items": [
    {
      "id": "item-123",
      "href": "/items/item-123"
    }
  ]
}
```

Search results MUST:

* reference existing LCAP resources
* preserve resource identity
* preserve resource semantics

Search results MUST NOT invent new resource representations.

---

## 8. Ranking and Ordering

Servers MAY rank search results.

Servers MAY return unranked results.

This specification defines no ranking model.

Clients MUST NOT infer:

* ranking methodology
* recommendation status
* resource quality

Result ordering is authoritative only for the response in which it appears.

---

## 9. Pagination

Search results MAY be paginated.

When pagination is used:

* pagination state MUST be explicit
* continuation information MUST be explicit
* total result counts MAY be omitted when unknown

Unknown totals MUST NOT be represented as zero.

---

## 10. Error Handling

Errors MUST be explicit and machine-readable.

Example:

```json
{
  "error": {
    "code": "invalid-query",
    "message": "Query syntax invalid"
  }
}
```

Servers MAY define additional error categories.

Clients MUST NOT infer search behavior from error responses.

---

## 11. Conformance Requirements

An implementation claiming conformance to the Search Profile MUST:

* be LCAP Core–conformant
* declare support explicitly
* expose search mechanisms explicitly
* represent search results as ordinary LCAP resources
* preserve resource identity
* avoid inference and silent fallback

An implementation MUST NOT claim conformance if it violates any requirement in this document.

---

## 12. Non-Goals and Explicit Exclusions

This specification MUST NOT define:

* recommendation systems
* relevance algorithms
* semantic search
* AI-generated search results
* user personalization
* analytics
* catalog federation

These exclusions are intentional and normative.

---

## 13. Stability and Evolution

LCAP Search Profile is frozen.

Future revisions:

* MUST preserve backward compatibility
* MUST NOT weaken Core semantics
* MUST NOT introduce inference
* MUST respect LCAP authority boundaries

Additional search functionality MUST be introduced through separate profiles.

---

## End of LCAP Search Profile
