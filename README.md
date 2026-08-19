# Compound Contribution Ledger

A compound interest calculator: what regular contributions grow into over time,
shown in both nominal and inflation-adjusted terms.

Live at **https://fredh2005.github.io/compound-calculator/**

## What it does

- **Starting age, withdrawal age, annual contribution, and an age to stop paying in** —
  so you can model contributing until 40 and letting it compound to 65.
- **Return and inflation sliders.**
- **Flat cash vs rise with inflation** — whether the payment stays the same number
  of pounds each year, or is uprated to hold its buying power.
- **Nominal vs today's money** for the headline figure.
- **A chart** of total balance against total contributed, with a hover readout for
  any single year.

## How the maths works

Contributions go in at the **start** of each year, so every payment earns a full
year of return. That is a growing annuity due:

```
FV at the end of contributions = C x (1+r) x ((1+r)^k - (1+g)^k) / (r - g)
then compounded for the remaining years:  x (1+r)^(n-k)
```

where `C` is the contribution, `r` the return, `g` the contribution growth rate
(inflation when uprating, zero when flat), `k` the years contributing and `n` the
total years. When `r == g` that expression is singular and the correct form is
`C x k x (1+r)^k`; the code handles it.

Verified against those closed forms across 20,000 randomised scenarios, worst
relative error ~5e-15, including the `r == g` singular case.

## Reading the result honestly

Switching contributions from flat to rising raises the headline a lot, but you are
also paying in far more pounds. **The fair comparison between the two modes is the
today's-money figure, not the nominal one.**

The arithmetic is exact; the projection is not. A constant annual return is a
fiction — real markets deliver the same average through very different paths, and
the order of good and bad years changes where you land. Not financial advice.

## Editing it

`index.html` is the whole thing — no build step, no dependencies, no framework.
Open it in a browser to test, commit, and GitHub Pages serves it.
