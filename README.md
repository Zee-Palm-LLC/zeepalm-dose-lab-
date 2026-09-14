# Dose Lab

**See what a supplement label actually contains.**

An interactive study from **Zee Palm Labs**. Built by [Zee Palm](https://zeepalm.com).

A proprietary blend legally hides the dose of every ingredient inside it. You get a
name, a total weight, and nothing else. This shows you the ceiling anyway.

> **Illustrative, not analytical.** Dose ranges are commonly cited effective ranges
> from human trials in healthy adults, summarised for teaching. Not medical,
> nutritional or regulatory advice. Every example product is invented.

## The idea

**21 CFR 101.36** lets a manufacturer hide individual doses inside a proprietary
blend, but it requires two things it cannot hide:

1. the blend's **total weight**, and
2. the ingredients listed in **descending order by weight**.

Those two rules produce a hard ceiling. If an ingredient is listed `k`th, every
ingredient above it weighs at least as much, so `k` of them together cannot exceed
the blend total:

```
ingredient(k) ≤ total ÷ k
```

When that ceiling lands below the researched effective dose, the shortfall is not an
estimate and not an accusation. It is arithmetic that follows from the label's own
declared numbers.

On a 2,400 mg blend with L-Citrulline listed second:

```
2 × citrulline ≤ 2,400 mg   ⇒   citrulline ≤ 1,200 mg
effective dose = 6,000 mg
⇒ at most 20% of a dose
```

## What it does

- **Nine vials in 3D**, one per ingredient, each filled to the fraction of *its own*
  effective dose that is actually present. An etched ring marks one full dose; a red
  column shows the gap
- **Every claim is derived**, step by step, in the panel — no conclusion without its
  working
- **A mass check** on the whole formula. Add up one effective dose of every active
  and compare it to the declared weight *and* to the serving size. A formula whose
  honest version outweighs its own scoop cannot be dosed properly at that serving
- **Edit any label** — change a dose, add an ingredient, switch the proprietary blend
  on or off, and watch every number move
- **A guided tour** at `#demo`, or the ▶ button — 26 seconds, then it hands control back

### Why every vial fills to the same line

Creatine at 5 g and zinc at 20 mg are three orders of magnitude apart. Plotting raw
mass would make everything but the largest ingredient invisible. Filling each vial to
its own target puts the ring at one height across the row, which is what makes a gap
readable at a glance.

## What it isn't

- **Not a lab assay.** It reads what a label declares. It cannot tell you what is in
  the tub
- **Not a compliance review.** "Provably short" describes only the arithmetic ceiling
  from the descending-order rule — a statement about what a declared blend weight can
  physically contain, never an allegation about a manufacturer
- **Not personalised.** No account is taken of body mass, stacking, tolerance or any
  medical condition, and reputable sources disagree at the margins
- **Not advice.** Speak to a doctor or a registered dietitian before changing what you take

## Running it

It is one static HTML file with no build step.

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

Three.js is loaded from a CDN; everything else — geometry, analysis, ingredient data —
is in the file. Nothing you type is sent anywhere.

## Privacy

There is no backend, no analytics and no storage. The page does one network request,
for the 3D library and the fonts.

## Licence

MIT — see [LICENSE](LICENSE). Fork it, restyle it, ship it on your own site.
