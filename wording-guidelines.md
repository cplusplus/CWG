# Wording Guidelines

Jens Maurer et al., 2025-03-02

This document offers a collection of guidelines for writing wording
targeted at integration into the ISO C++ Working Draft,
with a focus on core language wording (clauses 2-15).
The target audience is paper authors proposing changes to
the ISO C++ Working Draft.

These are guidelines, not hard-and-fast rules.
Sometimes, the subject matter is conducive to deviating from these guidelines.

## General

Read clause 4 [intro] of the Working Draft.
It provides the general framework for all detailed technical specifications.

The C++ Working Draft in its present form is
the result of more than 30 years of ongoing collaborative effort,
with changes being applied at least twice per year.
The existing wording thus varies in quality.
In general, newer wording better addresses the present expectations on
rigor and clarity than older wording.

Having an implementation of a new feature is great,
but does not imply that the specification is easy or
that the feature is easily implementable in other implementations.
Listen to implementers that utter concerns;
the target environments for implementations vary a lot.

Further reading:
- [ISO/IEC Directives, Part 2](https://www.iso.org/sites/directives/current/part2/index.xhtml)
- [Style guidelines for the Working Draft](https://github.com/cplusplus/draft/wiki/Specification-Style-Guidelines)


## Presentation

The purpose of suggested wording in your paper is to convey
the changes intended to be made to the Working Draft
to the wording review groups (CWG and LWG) and to the editors.
Specify the published version of the Working Draft (N-paper) your
changes are based on.
Specify any dependencies on other papers
that need to be applied before yours makes sense.

### Changes

In your paper, precede each chunk of wording with an introductory
sentence indicating where the words apply (section number and/or
stable label plus paragraph number).
Present wording as differences
(green underlined text for additions, red strikethrough text for deletions)
relative to the existing text in the working draft.
Quote sufficient context so that the editors can readily apply the changes
even when paragraph or section numbers have shifted;
a sentence or a bullet usually suffices for that.

The wording sections should be indented relative to the introductory
sentences.  The granularity of the differences should be the word; do
not try to present clever single-character changes.

Do not bother with numbering notes or examples; those will be
auto-numbered in the Working Draft anyway.

**Example**

> Modify [expr.shift] paragraph 3 as follows:
> > The value of `E1 >> E2` is <code>E1/2<sup>E2</sup></code>,
> > rounded <del>down</del> <ins>towards negative infinity</ins>.

(GitHub does not render colors.)

### Font styles

Use an approximation of the font styles used in the Working Draft.
In the interest of efficiency,
unchanged quoted text can ignore font variations.

- The defining appearance of a term or phrase is in *italics*;
other mentions are in regular font.
- Grammar non-terminals (e.g. _declarator-id_) are in *italics* everywhere.

## Structure

When adding a feature to the core language,
do not attempt to add a single subclause
that specifies the entirety of the feature.
Instead, start with the existing subclauses and
determine where updates are needed.

**Example:**
[basic.scope] covers all kinds of scopes,
[basic.lookup] specifies name lookup, and
[expr.prim.id] establishes the meaning of names
(in some cases, even when appearing outside of expressions).

Use math-like abstract concepts such as pairs (a bundle of two
things), tuples (a bundle of multiple things), sets (an unordered
collection of things), or lists (an ordered collection of things) as
necessary to convey a rule as precisely as possible.

Consider introducing definitions of terms and phrases to manage complexity.
Add cross-references when using a term or phrase
that could be mistaken as having the ordinary English meaning.
Within a single paragraph,
have at most one cross-reference to any given subclause.

Clearly differentiate definitions from normative rules,
for example by having them in separate sentences.

It is acceptable to introduce hypothetical C++ entities
such as types (e.g. closure types) or templates,
but all salient properties of such must be clearly specified.
For grammar non-terminals such as <I>template-head</I>,
the hypothetical definition is expected to have a valid token representation;
otherwise,
the abstract concept needs to be divorced from the grammar non-terminal
(see "exception specification" vs. _exception-specification_).

In library wording,
when specifying a complex component (e.g. RCU or hazard pointers),
spend a few paragraphs of introductory wording
to describe the data structure in the abstract,
possibly defining terms and phrases as necessary, and
then refer to the abstract description
in the specification of the individual classes and member functions.

### Notes, examples, and footnotes

Notes present statements of fact.
Use notes to highlight subtle consequences of the normative rules
and/or introduce cross-references to other parts of the standard.
Nesting an example inside a note is fine.
ISO disallows modal verbs such as "shall" or "may",
with the exception of "can", in notes.
Do not introduce normative rules in notes.
When referring to rules defined normatively elsewhere,
paraphrase the rule instead of trying to be precise; shorter is better.
Notes must be correct, but they need not be exhaustive.

**Example:**
> [ Note: The one-definition rule ([basic.def.odr]) prohibits X. -- end note]"

This adds a desirable cross-reference to the definition of the technical term;
the formulation does not preclude that the ODR also prohibits A, B, C beyond X.

Footnotes present ancillary information, establishing context beyond
the C++ Standard, such as trademark hints.
They should appear rarely.

Add examples to the Working Draft text.
Do not spend more than one example on basic syntactic exposition,
but do show surprising outcomes and interactions with other rules.
For syntax disambiguation rules, present an example of a tricky parse.

Prefer normative requirements if possible; this increases portability.
Sometimes, implementations cannot all provide a feature due to
environmental limitations or other concerns, but the standard should
still guide common implementations towards a desirable outcome.
For that case, prefix a paragraph with "*Recommended practice:*"
and use "should".

**Example:**

> *Recommended practice:*
> Implementations should not emit a warning
> that a name-independent declaration is used or unused.

### Conversions

When adding a new conversion, also check overload resolution for a
corresponding adjustment.

## Language

Use grammatical English.
Do not use contractions.
Do not use "you".

By default, use present tense and indicative form.

Hyphenate compound adjectives, e.g. "volatile-qualified".
Use the Oxford (or serial) comma.

In the core language,
"shall" is generally used to establish requirements on user programs:
"X shall be green" means the program is ill-formed if X is not green.
Exception: "The implementation shall ..." is a requirement on the implementation;
violation means non-conformance of the implementation.

In the standard library, "shall" establishes a precondition;
when violated, the program has undefined behavior.

Do not use "in" when nested constructs are not supposed to be in
scope.

**Example (bad):**
> X shall not appear in the expression

covers lambda bodies nested in the expression, which is often undesirable.

Use a recursive definition of a term or phrase to clearly specify how
a rule applies to a recursive construct such as an expression or
block.

Use "of" to uniquely identify top-level grammar components, without
risk of unwanted recursion.

**Example:**
> The _nested-name-specifier_ of a _qualified-id_ ...

does not cover any _nested-name-specifier_ nested
within the top-level _nested-name-specifier_.


## Specific words and phrases

<dl>
<dt>ill-formed, no diagnostic required</dt>
<dd>means that the standard does not
specify anything about the behavior at all, i.e. the behavior for such
a program is unbounded.
Use this when requiring a diagnostic is a hardship for compilers,
e.g. when different translation units are involved or
when analysis of uninstantiated templates would be needed.
</dd>

<dt>X is ill-formed</dt>
<dd>means the compiler is required to produce an error message for the program.
</dd>

<dt>X is conditionally-supported</dt>
<dd>means that the program is ill-formed if an implementation does not support X</dd>
</dt>

<dt>X is implementation-defined</dt>
<dd>means the implementation has freedom of choice,
but is required to document its choice of behavior.</dd>

<dt>the behavior is undefined</dt>
<dd>means there are no restrictions on the
program behavior if control flow reaches that particular point.</dd>

<dt>the behavior is erroneous</dt>
<dd>means the program may (or may not) terminate at any future time;
the behavior in case of non-termination must be specified</dd>

<dt>it is unspecified whether X or Y</dt>
<dd>means either X or Y can validly
happen, and each evaluation can make a different choice.
</dd>
</dl>

Avoid unbounded unspecified behavior.

**Example (bad):**

> If X happens, the behavior of the program is unspecified.

Do not try to make runtime behavior ill-formed; this is a category error.
