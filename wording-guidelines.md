# Wording Guidelines

Jens Maurer, 2025-02-27

This document offers a collection of guidelines for writing wording
targeted at integration into the ISO C++ Working Draft,
with a focus on core language wording (clauses 2-15).
The target audience is paper authors proposing changes to
the ISO C++ Working Draft.

These are guidelines, not hard-and-fast rules.  Sometimes, the subject
matter is conducive to deviating from these guidelines.

## General

Read clause 4 of the Working Draft.  It provides the general framework
for all detailed technical specifications.

The C++ Working Draft in its present form is the result of more than
30 years of ongoing collaborative effort, with changes being applied
at least twice per year.  The existing wording thus varies in quality.
In general, newer wording better addresses the present expectations on
rigor and clarity than older wording.

Having an implementation of a new feature is great, but does not imply
that the specification is easy or that the feature is easily
implementable in other implementations.  Listen to implementers that
utter concerns; the target environments for implementations vary a
lot.


## Presentation

In your paper, precede each chunk of wording with an introductory
sentence indicating where the words apply (section number and/or
stable label plus paragraph number).  Present wording as differences
(green underlined text for additions, red strikethrough text for
deletions) relative to the existing text in the working draft.  Quote
sufficient context so that the editors can readily apply the changes
even when paragraph or section numbers have shifted; a sentence or a
bullet usually suffices for that.

The wording sections should be indented relative to the introductory
sentences.  The granularity of the differences should be the word; do
not try to present clever single-character changes.

Do not bother with numbering notes or examples; those will be
auto-numbered in the Working Draft anyway.

Exactly the defining appearance of a term or phrase is in italics;
other mentions are in regular font.

## Structure

When adding a feature to the core language, do not attempt to add a
single subclause that specifies the entirety of the feature.  Instead,
start with the existing subclauses and determine where updates are
needed.  For example, [basic.scope] covers all kinds of scopes,
[basic.lookup] specifies name lookup, and [expr.prim.id] establishes
the meaning of names (in some cases, even when appearing outside of
expressions).

Consider introducing definitions of terms and phrases to manage
complexity.  Add cross-references when using a term or phrase that
could be mistaken has having the ordinary English meaning.  Within a
single paragraph, have at most one cross-reference to any given
subclause.

Notes present statements of fact.  Use notes to highlight subtle
consequences of the normative rules and/or introduce cross-references
to other parts of the standard.  Nesting an example inside a note is
fine.  ISO disallows modal verbs other than "can" in notes.  Do not
introduce normative rules in notes.  When referring to rules defined
normatively elsewhere, paraphrase the rule instead of trying to be
precise; shorter is better.  Notes must be correct, but they need not
be exhaustive.  Example: "[ Note: The one-definition rule
([basic.def.odr]) prohibits X. ]"  This adds a desirable
cross-reference to the definition of the technical term; the
formulation does not preclude that the ODR also prohibits A, B, C
beyond X.

Footnotes present anicillary information, establishing context beyond
the C++ Standard, such as trademark hints.  They should appear rarely.

Add examples to the Working Draft text.  Do not spend more than one
example on basic syntactic exposition, but do show surprising outcomes
and interactions with other rules. For syntax disambiguation rules,
present an example of a tricky parse.

Prefer normative requirements if possible; this increases portability.
Sometimes, implementations cannot all provide a feature due to
environmental limitations or other concerns, but the standard should
still guide common implementations towards a desirable outcome.  For
that case, prefix a paragraph with "Recommended practice:" and use
"should".

When adding a new conversion, also check overload resolution for a
corresponding adjustment.

## Language

Use grammatical English.  Do not use contractions.  Do not use "you".

By default, use present tense and indicative form.

Hyphenate compound adjectives.  Use the Oxford (or serial) comma.

In the core language, "shall" is generally used to establish
requirements on user programs: "X shall be green" means the program is
ill-formed if X is not green.  Exception: "The implementation shall
..." is a requirement on the implementation; violation means
non-conformance of the implementation.

In the standard library, "shall" establishes a precondition; when
violated, the program has undefined behavior.

Do not use "in" when nested constructs are not supposed to be in
scope.  Bad example: "X shall not appear in the expression" covers
lambda bodies nested in the expression, which is often undesirable.
Use a recursive definition of a term or phrase to clearly specify how
a rule applies to a recursive construct such as an expression or
block.

Use "of" to uniquely identify top-level grammar components, without
risk of unwanted recursion.  Example: "The _nested-name-specifier_ of
a _qualified-id_" does not cover any _nested-name-specifier_ nested
within the top-level _nested-name-specifier_.


## Specific words and phrases

"ill-formed, no diagnostic required" means that the standard does not
specify anything about the behavior at all, i.e. the behavior for such
a program is unbounded.  Use this when requiring a diagnostic is a
hardship for compilers, e.g. when different translation units are
involved.

"X is ill-formed" means the compiler produces an error message for the program.

"the behavior is undefined" means there are no restrictions on the
program behavior if control flow reaches that particular point.

"it is unspecified whether X or Y" means either X or Y can validly
happen, and each evaluation can make a different choice.  Avoid
unbounded unspecified behavior.

Do not try to make runtime behavior ill-formed; this is a category error.