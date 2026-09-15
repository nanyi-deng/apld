# Comparative Animal Protection Law Database (CAPLD)

*"CAPLD" is a working title, not yet finalized.*

> **Status: v0.1-draft — human verification pass in progress, not yet
> complete.** Every record already carries a `verification_tier` field
> stating whether *the AI-assisted retrieval step* fetched an official
> primary source (`verified`), relied on a secondary/search-snippet source
> (`snippet`), or drew on unconfirmed background knowledge (`unverified`).
> **That field describes sourcing, not human review.** No independent human
> spot-check of the coded content has been completed yet for this release —
> that pass is in progress using a structured audit protocol (see
> `docs/methodology.md`). Treat specific figures as provisional until a
> jurisdiction's records are confirmed; corrections will be issued as new
> versions with a changelog, not silently edited in place.

A structured, provision-level dataset comparing animal anti-cruelty / animal
protection law across 23 jurisdictions. Unlike existing country-level
scoring indices (e.g. the World Animal Protection Animal Protection Index)
or full-text legal archives (e.g. FAOLEX, the Global Animal Law Association
database), this dataset codes **penalty structure, scope of application,
enforcement mechanism, and linked policy-effect evidence** at the level of
individual statutory provisions — in a versioned, downloadable, codebook-
documented format. See `docs/methodology.md` for how this compares to
existing resources and to the policy-surveillance / legal-epidemiology
methodology this project draws on.

## Coverage (v0.1)

Mainland China, Taiwan, Hong Kong, Macau, Japan, South Korea, Singapore,
United States (federal), Canada (federal), England and Wales, Scotland,
Northern Ireland, the European Union, Germany, France, Switzerland, the
Netherlands, Italy, Spain, Australia (federal, New South Wales, Victoria),
and New Zealand.

## What's in this release

| File | Rows | Contents |
|---|---|---|
| `data/jurisdictions.csv` | 23 | Legal system, enforcement model, whether a general anti-cruelty offence exists |
| `data/legal_instruments.csv` | 39 | Statutes, regulations, and treaties, with source-verification tier |
| `data/provisions.csv` | 42 | Provision-level coding: penalty tiers, animal-scope classification, ancillary orders |
| `data/amendments.csv` | 30 | Reform history, with enactment date and effective date tracked separately |
| `data/sources.csv` | 39 | Every claim traces to a source with a retrieval date and verification tier |
| `data/policy_effect_studies.csv` | 23 | Registered evidence (or documented absence of evidence) on whether legal reforms produced measurable effects |
| `data/enforcement_statistics.csv` | 44 | Jurisdiction-year enforcement figures (prosecutions, convictions, arrests) for 10 jurisdictions with strong official time series |

`docs/data_dictionary.csv` documents every field and its controlled
vocabulary. `docs/methodology.md` explains the coding approach and its
limitations in full.

## A note on what "verified" means here

Every record in this dataset carries a `verification_tier` field:
**verified** (fetched directly from an official source), **snippet** (seen
only via a secondary source or search summary), or **unverified**
(background knowledge, not independently checked). This is a first-class,
published field — not an internal QA note — because a comparative legal
dataset that hides its own uncertainty is more dangerous than one that
states it plainly. Several widely-circulated claims about specific
jurisdictions' law were checked against primary sources during construction
and found to be incorrect; see `docs/methodology.md` for examples.

## What is *not* yet in this release

- `enforcement_statistics` covers 10 of the 23 jurisdictions so far (those
  with strong existing official time series: France, Germany, Japan,
  South Korea, Hong Kong, Australia NSW/VIC, Spain, England). The
  remaining 13 need dedicated retrieval work — several official sources
  (FBI NIBRS, Statistics Canada) are interactive tools that resist plain
  web scraping and need a direct API/CSV pull instead.
- Several jurisdictions still have known, explicitly flagged gaps (e.g.
  New Zealand's *current* consolidated statutory text remains blocked by
  a Cloudflare challenge that resists automated retrieval — a 2007
  official reprint was recovered instead, so current penalty figures rest
  on secondary sources rather than primary text). These are documented in
  each record's `notes` field, not silently smoothed over.
- A Chinese-language policy brief distilling findings for a legislative-
  reference audience is planned as a companion document, not yet written.

## Citation

See `CITATION.cff`. Data is licensed CC BY-SA 4.0 (`LICENSE_DATA.txt`);
repository code/tooling is MIT (`LICENSE`).

## Related work

This project is a sibling to the [Animal Harm Incident Database
(AHID)](https://github.com/nanyi-deng/animal-harm-incident-database), which
documents animal-harm *incidents* and judgments rather than the underlying
law. The two share a research program but code different objects.
