# thunder-bay-address-import

The **Thunder Bay city checkout** of the address-import family — city #10,
scaffolded 2026-08-16 by the breadth-first onboarding loop (engine
`future-work/multi-city/onboarding-queue.md`). Status: **import picked
2026-11-07** — the next city after Toronto and Guelph. No proposal
published, no uploads made. What to do next, in order:
[`IMPORT_CHECKLIST.md`](IMPORT_CHECKLIST.md). Drafts of the wiki page, the
forum post and the letters are in [`drafts/`](drafts/), unsent.

> "We acknowledge that Thunder Bay is built on the traditional territory of
> the Anishinabek, which includes the Ojibwa of Fort William First Nation,
> signatory to the Robinson-Superior Treaty of 1850. We also acknowledge the
> contributions of the Métis peoples." — the City of Thunder Bay's
> [land acknowledgement](https://www.thunderbay.ca/city-hall/history-heritage-and-records/history-of-thunder-bay/),
> quoted as published.

## Decisions (2026-11-07)

- **Fort William First Nation's addresses are included, as their own phase.**
  The City's layer carries 378 FWFN rows (`CITY = 'FWFN'`; 370 with a civic
  number, 8 without). They are a separate jurisdiction, so they upload only
  after FWFN has been written to and given time to answer, and never in the
  same changeset as a City tile. They already sit apart: outside every ward
  polygon, so `[city] orphan_name` puts them in their own tiles, named
  "Fort William First Nation". If FWFN says no, the phase is dropped and the
  wiki says so. Letter: [`drafts/fwfn-letter.md`](drafts/fwfn-letter.md).
- **One wiki proposal, not two projects.** Same source, licence, tooling and
  account; the FWFN phase has its own section, gate and changesets. There is
  no Canadian OSM precedent for importing on reserve land either way
  (research 2026-11-07, sources in the letter draft), so the page says what
  we did and why.
- **"Squaw Bay Rd" is not uploaded under that name.** 84 FWFN addresses are
  on it in the City's data. The word is a slur and much of Canada has been
  renaming it; the letter asks FWFN what the road is called. Until they
  answer, those 84 stay in the FWFN phase's review queue.
- **Land acknowledgement** in the wiki page and the forum post: the City's
  own published wording, quoted verbatim and linked (above), not one of our
  own. FWFN's website publishes none. Like the City's, it names no specific
  Métis organisation.

The pipeline lives in the engine repo,
[`address-importer-friend`](https://github.com/skfd/address-importer-friend)
(see its README for setup). This repo carries only Thunder Bay's
`config.toml`, credentials (`.env.*`, gitignored, from the `.example`
files), and — locally, gitignored — `data/` with the OSM extract and
`data/thunder-bay/tool.db`.

```bash
cd ../address-importer-friend
python run.py --city-dir ../thunder-bay-address-import
```

Source data: City of Thunder Bay municipal addresses via the sibling
[`ontario-address-changes`](https://github.com/skfd/ontario-address-changes)
tracker (`data/thunder-bay/thunder-bay.db`, 45,098 active rows / 44,022
civic addresses at snapshot 17, 2026-07-24). The survey's 2–3% way-share
and high missing rate make it a likely import target.

Thunder Bay was the portfolio survey's poster child for the
name-component-only street (canonical `street` = "BAILEY", 0% typed):
`street_from = "props:ROOT"` projects "BAILEY AVE" / "JAMES ST S" directly.
Its integer number column drops house qualifiers ("963" vs "963 1/2") — the
`number_from = "props:ADDRESS"` spec was added to the engine for it
(2026-08-16). No unit field exists (confirmed). **The FWFN question**: the
city layer publishes 378 Fort William First Nation addresses — a separate
jurisdiction; they surface as the exact orphan set of the 7-ward tile
fabric (99.16% coverage otherwise) and must be resolved before any upload.
Thunder Bay amalgamated Port Arthur and Fort William in 1970.

Entry state probed 2026-08-16 (`onboarding/entry-state-2026-08-16.json`):
**greenfield, the purest CanVec profile in the portfolio** — 985 of 1,006
sampled elements are CanVec 6.0 loose nodes (98% nodes, 16 ways), quiet
since Matthew Darwin's 2018 rename retag; the only steady local is
`eireidium` (POI mapping, 2022). No import tags, no wiki page, no recent
activity. Arguably the cleanest import target in the queue. Contacts:
Matthew Darwin, eireidium.

Before any production upload: wiki proposal page, forum announcement, and
feedback window per the
[OSM Import Guidelines](https://wiki.openstreetmap.org/wiki/Import/Guidelines)
— Toronto's [`IMPORT_PROPOSAL.mediawiki`](https://github.com/skfd/toronto-2-address-import/blob/main/IMPORT_PROPOSAL.mediawiki)
is the template.

MIT licensed.
