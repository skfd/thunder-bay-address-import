# thunder-bay-address-import

The **Thunder Bay city checkout** of the address-import family — city #10,
scaffolded 2026-08-16 by the breadth-first onboarding loop (engine
`future-work/multi-city/onboarding-queue.md`). Status: **onboarding**. No
proposal published, no uploads made; the config is a first draft for
conflation baseline runs.

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

Before any production upload: wiki proposal page, forum announcement, and
feedback window per the
[OSM Import Guidelines](https://wiki.openstreetmap.org/wiki/Import/Guidelines)
— Toronto's [`IMPORT_PROPOSAL.mediawiki`](https://github.com/skfd/toronto-2-address-import/blob/main/IMPORT_PROPOSAL.mediawiki)
is the template.

MIT licensed.
