# Reviewing the dose ranges

`data/ingredients.json` drives every claim this tool makes. One wrong `effectiveDose.low`
and the whole thing is dismissable, because the entire appeal is that the arithmetic is
not arguable. **Nothing in it has been checked by a qualified person yet.** Every entry
carries `"review": {"status": "unverified"}` until someone signs it off.

## Who should do it

One person, one sitting. In order of preference:

- A **registered dietitian** (RD / RDN in the US, RD in the UK) with a sports-nutrition
  interest — CSSD or ISSN-SNS certification is the marker
- A **sports nutrition academic** — anyone who has published on ergogenic aids
- Failing both, a **strength coach who reads the literature** is a weaker but real check

It is roughly a 45-minute job, not a research project. You are not asking anyone to derive
new numbers — only to confirm or correct a published range and attach a citation.

## What to ask for, exactly

> For each ingredient, is `effectiveDose.low` a defensible lower bound for the dose used in
> human trials in healthy adults? If not, what should it be, and what is your source?

`low` is the only number that matters. It is the threshold everything is measured against —
`high` is shown for context and never drives a verdict.

## Do these first

These appear in the three example labels, so they are the numbers the launch post stands on.
Everything else can be corrected after launch without embarrassment.

| Ingredient | effectiveDose.low | Evidence grade | Appears in |
| --- | --- | --- | --- |
| Niacin (vitamin B3) | 16 mg | caution | blend |
| Caffeine anhydrous | 200 mg | strong | blend, open |
| Beta-alanine | 3,200 mg | strong | blend, open |
| L-Citrulline | 6,000 mg | strong | blend, open |
| Betaine anhydrous | 2,400 mg | moderate | blend, open |
| Taurine | 1,000 mg | moderate | blend |
| L-Tyrosine | 500 mg | moderate | blend, open |
| Alpha-GPC | 300 mg | moderate | blend |
| Huperzine A | 50 mcg | weak | blend |
| Creatine monohydrate | 3,000 mg | strong | open |
| L-Theanine | 100 mg | moderate | open |
| Vitamin D3 | 1,000 IU | strong | greens |
| Magnesium | 200 mg | strong | greens |
| Zinc | 15 mg | strong | greens |
| Ashwagandha extract | 300 mg | moderate | greens |
| Rhodiola rosea | 200 mg | moderate | greens |
| L-Glutamine | 5,000 mg | weak | greens |
| Collagen peptides | 10,000 mg | moderate | greens |
| Beetroot extract | 500 mg | moderate | greens |
| Tribulus terrestris | 0 mg | none | greens |

## Lower priority

Selectable in the editor but not in any example label, so they only surface if a user picks them:

- BCAAs
- Citrulline malate (2:1)
- EPA + DHA
- HMB
- L-Arginine
- Sodium

## Recording the result

Fill in the `review` block per ingredient and open a PR:

```json
"review": {
  "status": "verified",
  "source": "Trexler et al. 2015, JISSN 12:30",
  "checkedBy": "A. Nutritionist RD, CSSD",
  "checkedOn": "2026-09-20"
}
```

`status` is one of `unverified`, `verified`, `corrected`. If a value changes, change it in
`effectiveDose` too — the tool reads that, not the review block.

## Three things to flag to the reviewer

1. **`evidence: "none"`** (currently only Tribulus terrestris) means no dose has been shown
   to produce the marketed effect. That is a strong claim — worth confirming they agree.
2. **`evidence: "caution"`** (currently only niacin) inverts the logic: the tool flags
   *excess* rather than shortfall. Check the threshold is the right one.
3. **`mgPerUnit`** converts a unit to milligrams and drives the blend arithmetic. Vitamin D
   (IU) and huperzine A (mcg) are the only non-trivial ones. A mistake here changes a verdict.
