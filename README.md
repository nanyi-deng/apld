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
protection law across 29 jurisdictions. Unlike existing country-level
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
United States (federal, California, Texas), Canada (federal, Ontario,
Quebec, British Columbia, Alberta), England and Wales, Scotland,
Northern Ireland, the European Union, Germany, France, Switzerland, the
Netherlands, Italy, Spain, Australia (federal, New South Wales,
Victoria), and New Zealand.

California, Texas, Ontario, and Quebec were added 2026-09-15 as their own
jurisdiction rows (not filed under the federal entry) because US states
and Canadian provinces have genuinely independent legislative authority
over criminal law here, mirroring how Australia's federal/state split is
already modeled (`AU-FED`/`AU-NSW`/`AU-VIC`) — unlike Mainland China's
municipal ordinances, which are filed under the single `CN` jurisdiction
because Chinese cities have no independent legal system of their own.

## What's in this release

| File | Rows | Contents |
|---|---|---|
| `data/jurisdictions.csv` | 29 | Legal system, enforcement model, whether a general anti-cruelty offence exists |
| `data/legal_instruments.csv` | 62 | Statutes, regulations, and treaties, with source-verification tier |
| `data/provisions.csv` | 74 | Provision-level coding: penalty tiers, animal-scope classification, ancillary orders, and (from 2026-09-15) its own row-level `verification_tier` |
| `data/amendments.csv` | 40 | Reform history, with enactment date and effective date tracked separately |
| `data/sources.csv` | 100 | Every claim traces to a source with a retrieval date and verification tier |
| `data/policy_effect_studies.csv` | 40 | Registered evidence (or documented absence of evidence) on whether legal reforms produced measurable effects, covering all 29 jurisdictions |
| `data/enforcement_statistics.csv` | 97 | Jurisdiction-year enforcement figures for 28 of 29 jurisdictions (EU excluded by design), including explicit confirmed-absence and inconclusive-search findings |

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

The US and Canada, by contrast, received genuine new jurisdiction rows
starting 2026-09-15: California and Texas (US), then Ontario, Quebec,
British Columbia, and Alberta (Canada), since American states and
Canadian provinces have independent legislative authority the way
Chinese cities do not. Findings include: California's felony-eligible
"wobbler" for animal cruelty applies to passive neglect, not only
intentional cruelty, with no prior-conviction gate — but California is
not a top-5 US state on ALDF's holistic ranking despite that specific
feature; Texas maintains two separate cruelty statutes (livestock vs.
non-livestock) with a first-offence felony ceiling of 10 years,
escalating to 20 on a repeat offence — the highest criminal exposure in
this dataset; Ontario's 2019 welfare-services law never uses "cruelty" as
an operative term and defines no "animal" at all; Quebec's celebrated
2015 Civil Code reform declaring animals "sentient beings" creates no
penalty of its own, and its actual penalty statute is fine-only for a
first offence at any severity; British Columbia applies one single flat
penalty ($75,000/2 years CAD) to every offence with no severity tiering
at all — tracing directly to the 2010 Whistler sled-dog cull and the
government task force it triggered; and Alberta currently has NO
imprisonment available for any offence, at any severity (a 2026 reform
raising this to 12 months awaits proclamation), and splits enforcement
three ways among two separate charities and a municipal government
department, the most fragmented enforcement model in this dataset. All
four Canadian provinces now on file converge on an outcome-based
"distress" standard as their actual operative legal term, regardless of
whether "cruelty" survives in the statute's title.

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
