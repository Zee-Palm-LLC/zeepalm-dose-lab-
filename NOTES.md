# Working notes

## Outside review — Sep 2026

Concept 8/10 · visual and demo quality 9/10. Reviewer's summary of what lands:

- The 3D tubes are the hook. Quantity is legible instantly instead of being another table.
- The problem is real — a label carries many ingredients at wildly different scales and
  there is no way to eyeball whether the formulation means anything.
- **The scoop-vs-dose comparison is the strongest moment.** It produces a "wait, what?".
- The progression (9 ingredients → ranking → dose analysis → formulation verdict) makes it
  read as a product rather than a visualisation.
- The tube metaphor is worth protecting. It is more memorable than another chat interface.

## The one real objection: stop saying "effective dose"

> For supplements there often isn't one universally correct effective dose. It depends on
> the ingredient, formulation, population, goal and the state of the evidence.

This is correct and it is the most important thing outstanding. Saying *"this ingredient
needs X mg to be effective"* is a claim we cannot defend per-person, and it is the single
easiest thing for a critic to pull on.

**What does not change:** the arithmetic. The `total ÷ k` ceiling from 21 CFR 101.36 is a
fact about what a declared blend weight can contain. That stays exactly as strong. Only the
*threshold* we compare it against needs to soften — and softening it actually makes the
comparison harder to argue with, because we stop asserting a number is universally right.

### The rewrite, concretely

| Now | Should be |
| --- | --- |
| "Effective dose 6,000 mg" | "Commonly studied 6,000–8,000 mg" |
| "1/9 at an effective dose" | "1/9 within the commonly studied range" |
| "At an effective dose" | "Within the studied range" |
| "Below effective range" | "Below the studied range" |
| "Provably short" | keep — it is an arithmetic statement, not a dose claim |
| "An honestly dosed version needs 13,616 mg" | "Matching the studied ranges would need 13,616 mg" |

In `data/ingredients.json`, rename `effectiveDose` → `referenceRange` and show **both** ends
in the detail panel rather than only `low`. Present it as:

    Commonly studied   6,000–8,000 mg
    On this label      ≤ 1,200 mg

and let the reader draw the conclusion, instead of the tool asserting it.

Pairs with REVIEW.md — the reviewer is already being asked to attach a citation per range.
Once `review.source` is populated, surface it in the detail panel. A visible citation is
what converts this from an opinion into a reference.

## Positioning

Not "a supplement dose checker". Closer to:

> **Understand what's actually inside your supplement.**

Which opens a longer pipeline than dosing alone:

    label → ingredients → dose → evidence → redundancy → formulation quality → assessment

"Redundancy" is the interesting unbuilt one — e.g. citrulline and arginine in the same
formula, or three overlapping stimulants — and nothing on the market shows it well.

## Order of work

1. The wording rewrite above. Cheap, and it is what stands between this and being trusted.
2. Dietitian sign-off per REVIEW.md, then show the citation in the UI.
3. Redundancy detection.
4. Only then, anything bigger.
