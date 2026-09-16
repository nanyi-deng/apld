# Methodology

## Why this dataset

Existing cross-national resources on animal protection law fall into two
categories, neither of which does what this dataset does. **Composite
scoring indices** — the World Animal Protection Animal Protection Index
(50 countries, letter grades A–G, last updated 2020), the Voiceless Animal
Cruelty Index (measures cruelty *outcomes* — slaughter and consumption
rates — not legal text at all, and stalled since 2020), and a 2026
econometric preprint (Animal Welfare and Policy Risk Index) — operate at
the level of country-wide letter grades or composite risk scores, never at
the level of what an individual statutory provision actually says. **Full-
text archives** — FAOLEX, the Global Animal Law Association database, the
Michigan State University Animal Legal & Historical Center — provide
statute text and citations but no comparative coding layer.

The Animal Legal Defense Fund's annual U.S. state rankings come closest to
genuine structured coding (56 jurisdictions, 20 categories, downloadable
annual report), but by design compares U.S. states against each other
within a single legal system — it cannot answer cross-national questions.

None of these combine (a) provision-level penalty quantification, (b)
enforcement-mechanism classification, and (c) linkage to policy-effect
evidence, in a versioned, downloadable, codebook-documented dataset. That
combination is this project's contribution.

## Coding framework

The coding approach is adapted from **policy surveillance / legal
epidemiology**, the methodology developed at Temple University's Center for
Public Health Law Research (LawAtlas.org) and applied in panel datasets
such as the State Firearm Laws database, PDAPS, and APIS. The core
methods reference is Anderson, E., Tremper, C., Thomas, S., & Wagenaar, A.C.
(2013). "Measuring statutory law and regulations for empirical research."
In A.C. Wagenaar & S. Burris (Eds.), *Public Health Law Research: Theory
and Methods* (pp. 237–260). Jossey-Bass.

This methodology has not previously been applied to animal protection law.
The one existing LawAtlas dataset touching companion animals (state rabies
vaccination laws) is framed as zoonotic-disease public health surveillance,
not animal welfare law. This project is, to the best of its author's
knowledge, the first application of a policy-surveillance coding protocol
to this legal domain.

## Solo-researcher reliability protocol

Standard policy-surveillance practice (the Delphi Standards for Policy
Surveillance, Presley et al. 2015, *Journal of Law, Medicine & Ethics*)
calls for 100% redundant double-coding — a standard assuming a funded,
multi-coder team. This dataset was built by a single researcher with AI-
assisted source retrieval. Rather than claim an unmet team standard, this
project follows a documented lower-resource precedent: the State Firearm
Laws database's original (pre-expansion) version was single-coded by its
principal investigator, with reliability maintained through cross-checking
against independently published secondary sources rather than a second
coder. This dataset follows the same pattern, adapted as a **blind re-
extraction consistency check**: a second, independent extraction pass is
run against the same primary sources without reference to the first pass's
results, and discrepancies are flagged for manual review rather than
silently reconciled.

## Source verification tiers

Every instrument, provision, amendment, and source record carries an
explicit `verification_tier`: **verified** (fetched directly from an
official government source), **snippet** (found only via a secondary
source or search-engine summary, not independently confirmed), or
**unverified** (background knowledge, not checked in this round). This
field ships with the published dataset, not as an internal working note.

This tiering caught concrete errors during construction. Two examples:

- A 2025 amendment to China's Public Security Administration Punishment
  Law is widely described in secondary sources as adding an "animal
  cruelty" provision. Direct retrieval of the official statutory text
  showed the new Article 89 does not contain the word for cruelty/abuse at
  all — it is a nuisance/dangerous-dog provision. The widely-circulated
  claim is incorrect.
- A claimed 2025 penalty-increase amendment in Taiwan, cited with specific
  figures and a named legislator, was traced back to the official
  legislative amendment history and found to be a misdated echo of a real
  2017 amendment — no such 2025 amendment occurred.

Neither error would have been caught by a coding process that treated
secondary-source claims as fact.

## Effective date vs. enactment date

Enactment date and effective date are tracked as separate fields, not
collapsed into one. Switzerland's Animal Welfare Act was passed by
parliament in December 2005 but did not take effect until September 2008
— a gap of nearly three years pending resolution of a competing popular
initiative. A dataset that recorded only one date would misplace this
jurisdiction's legal timeline by three years in any downstream analysis
using a jurisdiction-year panel structure.

## Policy-effect evidence: an honest evidence base

A systematic review of the empirical literature on whether animal-cruelty-
law reforms produce measurable effects (prosecution rates, sentencing
severity, enforcement outcomes) found the evidence base thin and
concentrated in three pockets: Australian quasi-experimental work (Morton,
Hebart & Whittaker and collaborators), descriptive U.S. research using FBI
NIBRS data as a data source rather than an evaluation target, and a recent
wave of East Asian and Central European judicial-decision content analyses
that are methodologically solid but not causal. A recurring finding across
independent sources (Australia, Hong Kong, South Korea, UK) is that
statutory maximum penalties rose sharply while sentences actually imposed
moved far less.

`policy_effect_studies.design_type` includes an explicit
`no_evaluation_found` value — used when a systematic search finds no
rigorous evaluation of a given reform. This is treated as a reportable
finding (how many reforms have never been evaluated), not a data gap to be
hidden.

## Known limitations

- This is a single-researcher project. Depth of verification varies by
  jurisdiction and, within a jurisdiction, by specific fact — see each
  record's `verification_tier` field (from 2026-09-15, `provisions.csv`
  carries its own row-level tier rather than only inheriting one from its
  parent instrument or source, following an independent audit that found
  a document-level tier can overstate confidence in a specific figure
  within it).
- The dataset currently covers 27 jurisdictions selected for a mix of
  legal systems and enforcement models, not for global representativeness.
  23 were selected as the original v1 scope; 4 more (California, Texas,
  Ontario, Quebec) were added 2026-09-15 as genuine sub-national
  jurisdictions — mirroring the existing `AU-FED`/`AU-NSW`/`AU-VIC` split
  — because US states and Canadian provinces have independent legislative
  authority over this area of law, unlike Mainland China's municipal
  ordinances, which stay filed under the single `CN` jurisdiction. Both
  evidence tables (`policy_effect_studies.csv`, `enforcement_statistics.csv`)
  were extended to cover all 4 new jurisdictions the same day; a
  misfiled Ontario row (originally attributed to `CA-FED`, written before
  `CA-ON` existed as its own jurisdiction) was corrected in the process.
- **Row granularity for `abandonment` and `fighting` is inconsistent
  across jurisdictions, and this is a structural limitation, not an
  oversight to be fixed by adding rows piecemeal.** Spain, Shanghai, and
  Guangzhou have standalone `abandonment` provision rows, and Canada and
  Italy have standalone `fighting` rows — not because other jurisdictions
  leave these conducts unregulated, but because this dataset creates one
  row per *statutory section*, and most jurisdictions fold abandonment
  and/or fighting into the same section as general cruelty or duty-of-care
  (e.g. Singapore's s.41C covers neglect and abandonment together;
  Victoria's s.9 folds wounding, confinement, and abandonment into one
  offence; Switzerland's Art. 26 lists animal fighting as one of five
  sub-offences in a single article; Beijing's Art. 17(9) and China's new
  Chengdu ordinance both bundle abuse and abandonment in one clause).
  **Do not count standalone `abandonment`/`fighting` rows as a
  jurisdiction-comparison metric** — read the `notes` field of that
  jurisdiction's `general_cruelty` or `neglect_duty_of_care` rows first,
  since the conduct is very often covered there instead.
- A handful of date fields are intentionally blank rather than
  fabricated — see `data_dictionary.csv` for `provisions.effective_date`
  and `amendments.enactment_date`/`effective_date`, each of which
  documents why (day/month not confirmed, or no single date applies to a
  bundled amendment).
- Two "confirmed absence" findings originally coded to this dataset's
  strictest evidentiary bar were downgraded on 2026-09-15 audit review
  because their own caveats admitted an incomplete search: Taiwan's
  enforcement-statistics entry (recoded `search_inconclusive`, a
  distinct value from `no_official_statistics_published`, because a
  competing unconfirmed claim exists that data is published) and a
  Mainland China policy-effect entry on the Shenzhen/Zhuhai
  cat-and-dog-meat bans (`verification_tier` downgraded from `verified`
  to `snippet`, the lower of the two tiers this table uses).
