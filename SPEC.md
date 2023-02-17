# Regular JSON
## v0.1 - 2023-02-17

This document defines *Regular JSON*, a family of strict subsets of JSON as
specified in [RFC 8259](https://www.rfc-editor.org/rfc/rfc8259.html). Regular
JSON is constrained to be a *regular language*, for use in constrained
environments and security-sensitive applications.

## Regular JSON, briefly

All JSON terms used in this specification are defined in reference to RFC 8259.

Regular JSON achieves regularity by placing constraints on the maximum nesting
depth of JSON constructs. It is a family of JSON subsets ranked according to
the maximum nesting of terms. The definition is inductive:

 * _Rank 0 Regular JSON_ consists of simple scalar values only:
    - The Boolean values `true` and `false`
    - `null`
    - Numbers, limited to the range [-2^53, 2^53]. Numbers outside this range
      MUST be rejected.
    - Strings
 * _Rank n Regular JSON_ (for *n* > 0) consists of:
    - Rank 0 Regular JSON values
    - Arrays, all elements of which are *Rank (n-1) Regular JSON* values.
    - Objects, all values of which are *Rank (n-1) Regular JSON* values.

For example, *Rank 1 Regular JSON* allows arrays and objects whose values are
all simple scalar objects. *Rank 2 Regular JSON* additionally allows Rank 1
objects or arrays as values, and so on.
