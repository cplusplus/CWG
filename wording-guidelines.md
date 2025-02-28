# Wording Guidelines

Jens Maurer et al., 2025-02-28

This document offers a collection of guidelines for writing wording
targeted at integration into the [ISO C++ Working Draft][draft],
with a focus on core language wording
(clauses [[intro.refs]](https://eel.is/c++draft/intro.refs) through
[[cpp]](https://eel.is/c++draft/cpp)).
The target audience is paper authors proposing changes to
the ISO C++ Working Draft.

These are guidelines, not hard-and-fast rules.
Sometimes, the subject matter is conducive to deviating from these guidelines.

## General

Read clause [[intro]](https://eel.is/c++draft/intro) of the Working Draft.
It provides the general framework for all detailed technical specifications.

The C++ Working Draft in its present form is the result of more than
30 years of ongoing collaborative effort, with changes being applied
at least twice per year.
The existing wording thus varies in quality.
In general, newer wording better addresses
the present expectations on rigor and clarity than older wording.

Having an implementation of a new feature is great,
but does not imply that the specification is easy or that the feature is easily
implementable in other implementations.
Listen to implementers that utter concerns;
the target environments for implementations vary a lot.


## Presentation

The purpose of suggested wording in your paper is to convey to the editors
what changes shall be made to the working draft.
Therefore, you need to specify

- which published version of the working draft your changes are relative to,
  optionally including changes in other papers,
- which sections of the existing wording are modified, and
- precisely where new wording is to be inserted.

**Example:**

> The following changes are relative to [N5001],
> including the changes from [P1234].

### Presenting changes

Precede each chunk of wording changes with an introductory
sentence indicating where the words apply (section number and/or
stable label plus paragraph number).
Present wording as differences
(red strikethrough text for deletions, green underlined text for additions)
relative to the existing text in the working draft.  Quote
sufficient context so that the editors can readily apply the changes
even when paragraph or section numbers have shifted; a sentence or a
bullet usually suffices for that.

The wording sections should be indented relative to the introductory
sentences.  The granularity of the differences should be the word; do
not try to present clever single-character changes.

**Example**:

> Modify [[expr.shift]](https://eel.is/c++draft/expr.shift#3)
> paragraph 3
> as follows:
>
> > The value of `E1 >> E2` is <code>E1/2<sup>E2</sup></code>,
> > rounded <del>down</del> <ins>towards negative infinity</ins>.

**Note:**
<del>down</del> should be red, and <ins>towards negative infinity</ins>
should be green,
even though GitHub doesn't render them as such.

Do not bother with numbering notes or examples; those will be
auto-numbered in the Working Draft anyway.

### Font styles

In your proposed wording,
you should follow the style of the working draft, meaning:

- The defining appearance of a term or phrase is *italic*
  (subsequent mentions have regular style).
- Inline C++ snippets use `code font`.
- Grammatical terms (e.g. *declaration*) are italic, sans-serif.


## Structure

When adding a feature to the core language, do not attempt to add a
single subclause that specifies the entirety of the feature.
Instead, start with the existing subclauses and determine where updates are
needed.

**Example:**
[[basic.scope]](https://eel.is/c++draft/basic.scope) covers all kinds of scopes,
[[basic.lookup]](https://eel.is/c++draft/basic.lookup) specifies name lookup, and
[[expr.prim.id]](https://eel.is/c++draft/expr.prim.id) establishes the meaning of names
(in some cases, even when appearing outside of expressions).

Consider introducing definitions of terms and phrases to manage
complexity.
Add cross-references when using a term or phrase that
could be mistaken has having the ordinary English meaning.
Within a single paragraph,
have at most one cross-reference to any given subclause.

### Notes, examples, and footnotes

Notes present statements of fact.
Use notes to highlight subtle consequences of the normative rules
and/or introduce cross-references to other parts of the standard.

Nesting an example inside a note is fine.
ISO disallows modal verbs other than "can" in notes
("shall", "may", etc.).
Do not introduce normative rules in notes.
When referring to rules defined normatively elsewhere,
paraphrase the rule instead of trying to be
precise; shorter is better.
Notes must be correct, but they need not be exhaustive.

**Example:**

> [ *Note*: The one-definition rule ([basic.def.odr]) prohibits X. ]

This adds a desirable
cross-reference to the definition of the technical term; the
formulation does not preclude that the ODR also prohibits A, B, C
beyond X.

Footnotes present anicillary information, establishing context beyond
the C++ Standard, such as trademark hints.  They should appear rarely.

Add examples to the Working Draft text.  Do not spend more than one
example on basic syntactic exposition, but do show surprising outcomes
and interactions with other rules. For syntax disambiguation rules,
present an example of a tricky parse.

### Normative requirements and recommendations

Prefer normative requirements if possible; this increases portability.

Sometimes, implementations cannot all provide a feature due to
environmental limitations or other concerns, but the standard should
still guide common implementations towards a desirable outcome.
For that case, prefix a paragraph with "*Recommended practice*:" and use "should".

**Example:** ([[intro.abstract] paragraph 6](https://eel.is/c++draft/intro.abstract#6))

> *Recommended practice*:
> An implementation should issue a diagnostic when such an operation is executed.

### Changes to conversions

When adding a new conversion ([[conv]](https://eel.is/c++draft/conv))
or changing the behavior of an existing one,
also check overload resolution for a corresponding adjustment.

## Language

Use grammatical English.
Do not use contractions.
Do not use "you".

By default, use present tense and indicative form.

Hyphenate compound adjectives (e.g. volatile-qualified).
Use the Oxford (or serial) comma.

The wording in the C++ Standard adheres to
[ISO/IEC Principles and rules for the structure and drafting of ISO and IEC documents][iso-principles],
and so should any wording you propose.
See also the
[C++ Working Draft Specification Style Guidelines][style-guidelines].

In the core language, "shall" is generally used to establish
requirements on user programs: "X shall be green" means the program is
ill-formed if X is not green.

**Exception:**
"The implementation shall
..." is a requirement on the implementation; violation means
non-conformance of the implementation.

In the standard library, "shall" establishes a precondition; when
violated, the program has undefined behavior.

Do not use "in" when nested constructs are not supposed to be in
scope.

**Example (bad):**
"X shall not appear in the expression"
covers lambda bodies nested in the expression, which is often undesirable.

Use a recursive definition of a term or phrase to clearly specify how
a rule applies to a recursive construct such as an expression or
block.

Use "of" to uniquely identify top-level grammar components,
without risk of unwanted recursion.

**Example:**

> The _nested-name-specifier_ of a _qualified-id_"
> does not cover any _nested-name-specifier_
> nested within the top-level _nested-name-specifier_.


## Specific words and phrases

<dl>
<dt>X is ill-formed
(<a href="https://eel.is/c++draft/defns.ill.formed">[defns.ill.formed]</a>)</dt>
<dd>
means the compiler produces an error message for the program
</dd>
<dt>ill-formed, no diagnostic required</dt>
<dd>
means that the standard does not
specify anything about the behavior at all, i.e. the behavior for such
a program is unbounded.  Use this when requiring a diagnostic is a
hardship for compilers, e.g. when different translation units are
involved.
</dd>
<dt>the behavior is undefined
(<a href="https://eel.is/c++draft/defns.undefined">[defns.undefined]</a>)</dt>
<dd>
means there are no restrictions on the
program behavior if control flow reaches that particular point.
</dd>
<dt>it is implementation-defined whether X or Y
(<a href="https://eel.is/c++draft/defns.impl.defined">[defns.impl.defined]</a>)</dt>
<dd>
means either X or Y can validly happen,
and the implementation is required to document what happens.
</dd>
<dt>it is unspecified whether X or Y
(<a href="https://eel.is/c++draft/defns.unspecified">[defns.unspecified]</a></dt>
<dd>
means either X or Y can validly happen,
and each evaluation can make a different choice.
</dd>
</dl>

Avoid unbounded unspecified behavior.

**Example (bad):**

> If X happens, the behavior of the program is unspecified.

Do not try to make runtime behavior ill-formed; this is a category error.


[draft]: https://github.com/cplusplus/draft/
[iso-principles]: https://www.iso.org/sites/directives/current/part2/index.xhtml
[style-guidelines]: https://github.com/cplusplus/draft/wiki/Specification-Style-Guidelines
