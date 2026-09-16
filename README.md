# Animal Protection Law Database (APLD)


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
| `data/legal_instruments.csv` | 53 | Statutes, regulations, and treaties, with source-verification tier |
| `data/provisions.csv` | 58 | Provision-level coding: penalty tiers, animal-scope classification, ancillary orders, and (from 2026-09-15) its own row-level `verification_tier` |
| `data/amendments.csv` | 30 | Reform history, with enactment date and effective date tracked separately |
| `data/sources.csv` | 61 | Every claim traces to a source with a retrieval date and verification tier |
| `data/policy_effect_studies.csv` | 35 | Registered evidence (or documented absence of evidence) on whether legal reforms produced measurable effects, covering all 23 jurisdictions |
| `data/enforcement_statistics.csv` | 67 | Jurisdiction-year enforcement figures for 22 of 23 jurisdictions (EU excluded by design), including explicit confirmed-absence and inconclusive-search findings |

`docs/data_dictionary.csv` documents every field and its controlled
vocabulary. `docs/methodology.md` explains the coding approach and its
limitations in full, including a 2026-09-15 independent-audit section
covering what was checked, what was found and fixed, and what remains open.

Mainland China's own patchwork of law received deeper coverage on
2026-09-15: Tianjin (2020-02-14) and Fujian (2020-02-18) passed the
earliest provincial-level wildlife-consumption bans, using a named-
category mechanism; a 2020-02-24 national NPC Standing Committee Decision
then introduced the livestock-catalogue whitelist mechanism (the
traceable legal trigger for every ordinance that followed it, not
something localities had already converged on independently), prompting
Shenzhen, Zhuhai, Guangzhou, and Beijing to each pass supporting local
legislation within about two months — all excluding cats/dogs by omission
from a food-species whitelist rather than
naming them, contrary to widespread media framing — while Shanghai
repealed its old wildlife law in the same window but did not pass a
replacement until 2023. Separately, municipal dog-keeping ordinances in
Beijing, Shanghai, Guangzhou, and Chengdu explicitly prohibit
abusing/abandoning a dog; two of the four cities' abuse clauses (Beijing,
Shanghai) were confirmed, by checking every cross-reference in their
penalty chapters, to carry no attached penalty at all — a real enforcement
gap, not a coding gap. A voluntary national zoo-management standard names
animal welfare as a purpose and bans wildlife performances, but has no
enforcement mechanism of its own. All of this is filed under the single
`CN` jurisdiction rather than as separate sub-national jurisdictions,
since these are supplementary municipal/national regulations, not
independent legal systems.

## A note on what "verified" means here

Every record in this dataset carries a `verification_tier` field:
**verified** (fetched directly from an official source), **snippet** (seen
only via a secondary source or search summary), or **unverified**
(background knowledge, not independently checked). This is a first-class,
published field — not an internal QA note — because a comparative legal
dataset that hides its own uncertainty is more dangerous than one that
states it plainly. Several widely-circulated claims about specific
jurisdictions' law were checked against primary sources during construction
and found to be incorrect; see `docs/methodology.md` for examples. As of
2026-09-15, `provisions.csv` carries this tier at the row level rather than
only inheriting one from its parent legal instrument or source, after an
independent audit found that a document-level tier can overstate confidence
in a specific figure within it.

## What is *not* yet in this release

- Row granularity for `abandonment` and `fighting` conduct is uneven across
  jurisdictions by design of the schema (one row per statutory section) —
  see `docs/methodology.md`'s Known Limitations section before using
  standalone-row counts as a cross-jurisdiction comparison.
- Several jurisdictions still have known, explicitly flagged gaps (e.g.
  New Zealand's *current* consolidated statutory text remains blocked by
  a Cloudflare challenge that resists automated retrieval — a 2007
  official reprint was recovered instead, so current penalty figures rest
  on secondary sources rather than primary text; Macau's sources needed
  a proxy-mirror fetch after every direct attempt failed). These are
  documented in each record's `notes` field, not silently smoothed over.
- US federal enforcement data (2016–2020) comes from a peer-reviewed
  academic compilation of FBI NIBRS data rather than an FBI publication
  directly — 2021–2024 need a free api.data.gov key this project hasn't
  obtained yet.
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
