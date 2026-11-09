# Thunder Bay import checklist

The order to do things in, from picking the city (2026-11-07) to the last
upload. Each step says who does it: **you** (the operator), or **Claude** in a
session. Ticked steps are done.

Where things are:
- the decisions behind this list: [README](README.md#decisions-2026-11-07);
- the wiki page draft: [`IMPORT_PROPOSAL.mediawiki`](IMPORT_PROPOSAL.mediawiki);
- the forum post and letters: [`drafts/`](drafts/).

## Phase 0 — Data and baseline (Claude)

- [x] **1.** Decide on Fort William First Nation: included, as its own gated
      phase (README).
- [x] **2.** Name the FWFN tiles: `[city] orphan_name`, engine `ac0834ce`.
- [x] **3.** Refresh the OSM extract and build the tiles (2026-11-08). The
      extract is the 2026-11-06 Geofabrik PBF. 122 tiles. All 378 FWFN rows
      are in 9 FWFN-only tiles. Getting there took two engine fixes
      (`7ba960ed`): small FWFN tiles were being merged into Westfort tiles,
      and Westfort's tile polygon had lost the hole around FWFN land.
- [x] **4.** Baseline over every tile (2026-11-08): 45,098 candidates; 322
      MATCH, 27 MATCH_FAR, **44,740 MISSING** (44,379 City + 361 FWFN), 9
      skipped for having no civic number (engine `f46ba360`); 894 waiting
      for review. Numbers filled into the drafts.

Found on the way, and now in the drafts:
- **OSM's Thunder Bay addressing is CanVec interpolation.** 6,604 range
  ways, whose endpoints are 12,763 of the 12,950 address nodes. The engine
  ignores endpoints when matching, so nearly every City address is MISSING,
  and the new points would sit alongside the ranges. The wiki draft proposes
  points first, then retiring fully covered ranges as a separate reviewed
  step (§ CanVec interpolation).
- **"Squaw Bay Road" is already in OSM**, on 2 CanVec nodes on FWFN land.
- **4 City addresses sit exactly on an edge between two ward tiles**:
  147 Amelia St W, 502 Norah St S, 130 Inglewood Cres, 111 Machar Ave. They
  are in two runs each, so upload them from one run and reject them in the
  other.

## Phase 1 — Read the baseline (you, ~1 hour)

- [ ] **5.** Open the engine on this checkout and look at the map and the
      biggest tiles: `cd ../address-importer-friend && python run.py --city-dir ../thunder-bay-address-import`.
      Is the gap where you'd expect it?
- [ ] **6.** Read one dense tile's review queue end to end, especially
      `MATCH_FAR` and `nearby_street_mismatch`. That's where CanVec spelling
      variants will show.
- [x] **7.** Pilot tile: `mckellar-sw-sw-ne`, downtown Fort William, 495
      candidates, 493 missing (confirmed 2026-11-08).

## Phase 2 — Decisions only you can make

- [x] **8.** FWFN wait: 30 days; no reply means Phase 3 is skipped
      (2026-11-08).
- [x] **9.** `270-1` numbers: split into `addr:housenumber` + `addr:unit`
      (2026-11-08). Engine `32528ac8`, `[source_fields] unit =
      "number-after-hyphen"`, `[units] policy = "per-door-or-collapse"`. The
      14 Caribou Cres rows are 14 door nodes; nothing else moved.
- [x] **9a.** CanVec ranges: the import doesn't touch interpolation. Cleanup
      comes later through against-interpolation (MapRoulette, line by line),
      with its own forum post. Needs a `config.thunder-bay.toml` there when
      the time comes.
- [x] **9b.** Land acknowledgement: version D (2026-11-08). It names the land
      and FWFN, mentions the treaty only as a place, and adds our own
      sentence: First Nations should have more say in, and ownership of, how
      their traditional lands beyond their reserves are developed.
- [x] **9c.** [Contributors#Canada](https://wiki.openstreetmap.org/wiki/Contributors#Canada):
      the Thunder Bay entry now carries the licence's required sentence and
      the new licence URL (saved by Skfd 2026-11-08 18:32 UTC).
- [ ] **10.** Read all four drafts. Change anything that doesn't sound like you.

## Phase 3 — Engine work before announcing (Claude)

- [x] **11.** **Engine TODO §7: tile ids must survive a rebuild.** Decided
      2026-11-08: freeze Thunder Bay's tiles for the whole import, instead of
      building re-association. `[tiles] frozen` in `config.toml` makes
      `tiles_build` refuse to run (engine `d83652e1`). The 122 tiles of
      2026-11-08 stay. A copy is in [`frozen-tiles/`](frozen-tiles/). If
      `data/` is lost, copy `tiles.json` back to `data/thunder-bay/` and
      `meta.json` to `data/thunder-bay/tiles/`. New snapshots still reach
      new runs through each tile's polygon. Only `/map`'s address counts go
      stale.
- [x] **12.** The 9 `fort-william-first-nation-*` runs from the baseline were
      deleted the same night (2026-11-08), so the review UI holds no FWFN
      candidate one click from upload. Their numbers are kept in step 4 (361
      missing, 8 skipped). Before Phase 6, re-run those tiles with fresh data
      and the Nation's answers.

## Phase 4 — Outreach (you)

Order matters: FWFN and the local mappers hear from you before the forum does.
Only step 10 has to come first, because these go out under your name. Steps 5
and 6 gate the pilot upload (step 18), not the outreach, so do them during the
FWFN wait and the forum window (decided 2026-11-08).

All of it went out the same night, 2026-11-08, rather than spread over days.

- [x] **13.** Wiki page published 2026-11-08 (04:33 UTC):
      <https://wiki.openstreetmap.org/wiki/Thunder_Bay/Address_Import>,
      status Proposed. `IMPORT_PROPOSAL.mediawiki` matches what was saved.
- [ ] **13a.** Add the page to [[Import/Catalogue]].
- [x] **14.** FWFN letter sent 2026-11-08 from toronto@comentality.com. No
      reply by **2026-12-08** means Phase 6 is skipped.
- [x] **15.** Notes to Matthew Darwin and eireidium sent from `skfd`
      2026-11-08 (04:35 UTC).
- [x] **16.** Forum announcement posted 2026-11-08:
      <https://community.openstreetmap.org/t/thunder-bay-address-import-proposal-for-review/149917>. The 14-day window closes **2026-11-22**.
- [x] **17.** `[export] import_plan` in `config.toml` is the wiki URL, set
      2026-11-08 ahead of publishing; the drafts carry the same link.

## Phase 5 — Production, City only

- [ ] **18.** Day 15 (2026-11-23) or later, with no objection left unanswered: upload the
      pilot tile from `skfd imports` (`run.py --prod`). Stop. Look at it in iD
      and JOSM, and read the changeset.
- [ ] **19.** One-week hold. Then ward by ward, one tile per changeset, at most
      one a minute.
- [ ] **20.** Publish a DB snapshot after the pilot (`/publish-db ../thunder-bay-address-import`)
      and after each ward.
- [ ] **21.** Watch the forum thread and the account history; answer within a
      day.

## Phase 6 — Fort William First Nation

- [ ] **22.** Upload only when step 8's condition is met. Apply anything the
      Nation asked for: names, spellings, a subset. If they said no, write that
      on the wiki and drop the phase.
- [ ] **23.** Separate changesets, the FWFN tiles only. The comment template
      (`[upload] changeset_comment_template`) stamps them "Thunder Bay Open
      Data address import". The data is the City's, so that's accurate, but
      you may want a comment that also names Fort William First Nation for
      this phase.

## Phase 7 — Close and maintain

- [ ] **24.** Closing report on the wiki page and the forum thread.
- [ ] **25.** Add `[maintenance] since = "<date>"` to `config.toml` and copy the
      engine's `scripts/maintenance-reminder.caller.yml` to
      `.github/workflows/maintenance-reminder.yml`. From then on, a reminder
      issue arrives on the 1st of each month.
