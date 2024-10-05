# Artifacts for Transporting Theorems about Typeability in LF Across Schematically Defined Contexts

This repository contains the artifacts for the paper "Transporting Theorems
about Typeability in LF Across Schematically Defined Contexts." This includes
Adelfa proofs and encoded signatures for various examples. In order to run these
files, you will need to have the Adelfa proof assistant installed. You can find
instructions for installing Adelfa [on its
webpage](https://adelfa-prover.org/download). These artifacts require the
development version of Adelfa, so one must use the git method or equivalently
build it from source.

The proof rule presented in Section 5.2 is built into Adelfa's
[`apply`](https://adelfa-prover.org/reference-guide/tactics#apply-name-to-hyp-names-with-bindings)
tactic. In its simplest form, the `apply` tactic takes two hypotheses or lemmas
of the form $F \supset B$ and $F$ and produces the conclusion $B$ from
them. The matching of the antecedent of the implication and a given hypothesis
or lemma can be more complex. In the version relevant to this artifact, this
matching builds in the transport proof rule as well, i.e., it allows the proof
rule in the paper to "lift" the hypothesis or lemma before using it in the
application. More specifically, when the `apply` tactic is invoked, Adelfa will
attempt to match the context variable within the theorem with the one quantified
in the lemma. This matching will succeed when the proof rule is derivable.

In each example, we will denote where the new capability is required in order
for `apply` to succeed.

## ORBI Benchmarks

- Figure 2 is translated into an Adelfa signature in the file
  [`equal-untyped.lf`](/equal-untyped/equal-untyped.lf).
- Example 1 is the `reflG` theorem in the file
  [`equal-untyped-new.ath`](/equal-untyped/equal-untyped-new.ath) on line 12.
- We provide two versions of Section 6's property, named `ceqG`.
  - Schema subsumption is used in [`equal-untyped-new.ath`](/equal-untyped/equal-untyped-new.ath).
  - The proof without schema subsumption is played out in [`equal-untyped-old.ath`](/equal-untyped/equal-untyped-old.ath)

## POPLmark

This example is that of proving the transitivity of subtyping. The Twelf proof
provided by Michael Ashley-Rollman, Karl Crary, and Robert Harper proves the
main theorems with a richer structure for contexts designed to ensure adequacy,
but then changes the structure of the context to a simpler and more intuitive
form using subordination. We provide that Twelf development in
[`1a.elf`](/poplmark/1a.ath). The related exercise carried out in Adelfa is to
be found in [`1a.ath`](/poplmark/1a.ath). Here, schema subsumption is used to
transform the original result into the more palatable form.

## Size

This example proves a theorem that asserts that the size of a lambda term does
not decrease under a substitution. Proving a theorem of this kind requires
properties of addition pertaining to natural numbers that hold in an empty
context. However, induction over the structure of lambda terms requires
reasoning about sizes of terms to be done within nonempty contexts. Properties
about addition are needed within such contexts and the relevant lemmas must
therefore be transported to them. The complete development is to be found in
[`size.ath`](/size/size.ath).
