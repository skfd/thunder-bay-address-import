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
- [ ] **3.** Refresh the OSM extract (`python -m t2.osm_refresh`) and build
      the tiles (`python -m t2.tiles_build`). Check that the FWFN tiles hold
      exactly the 378 `CITY = 'FWFN'` rows.
- [ ] **4.** Run the baseline over every tile (`python -m t2.run_for_all`),
      then fill the `{{TBD}}` numbers in the wiki draft and `{MISSING}` in the
      forum draft.

## Phase 1 — Read the baseline (you, ~1 hour)

- [ ] **5.** Open the engine on this checkout and look at the map and the
      biggest tiles: `cd ../address-importer-friend && python run.py --city-dir ../thunder-bay-address-import`.
      Is the gap where you'd expect it?
- [ ] **6.** Read one dense tile's review queue end to end, especially
      `MATCH_FAR` and `nearby_street_mismatch`. That's where CanVec spelling
      variants will show.
- [ ] **7.** Pick the pilot tile: one dense City tile, 250–750 candidates,
      **not** an FWFN tile. Write its name into the wiki draft.

## Phase 2 — Decisions only you can make

- [ ] **8.** **The FWFN wait.** How long after the letter before Phase 3 can
      go ahead without a reply, and whether it can at all. The research
      suggested ≥30 days, a phone call around day 30, and going ahead around
      day 45. That's a suggestion, not an OSM norm. Write your answer into the
      letter (`{wait}`) and the wiki draft.
- [ ] **9.** **The `123-4` numbers** (14 rows): leave as an open question on the
      wiki (as drafted), or decide now.
- [ ] **10.** Read all four drafts. Change anything that doesn't sound like you.

## Phase 3 — Engine work before announcing (Claude)

- [ ] **11.** **Engine TODO §7: tile ids must survive a rebuild.** The engine's
      TODO says "before announcing any import". Today a tile rebuild orphans
      every run's tile. Build the spatial re-association, or decide explicitly
      to freeze Thunder Bay's tiles for the whole import.
- [ ] **12.** Hold the 84 "Squaw Bay Rd" addresses and the 8 number-less FWFN
      rows out of any run, whatever else happens. Check this in the FWFN tiles'
      review queue.

## Phase 4 — Outreach (you)

Order matters: FWFN and the local mappers hear from you before the forum does.

- [ ] **13.** Publish the wiki page at `Thunder_Bay/Address_Import` from
      `IMPORT_PROPOSAL.mediawiki`, still with status Proposed. Add it to
      [[Import/Catalogue]].
- [ ] **14.** Send the FWFN letter (`drafts/fwfn-letter.md`) with the wiki
      link. Note the date on the wiki page.
- [ ] **15.** Send the two notes to local mappers (`drafts/local-mappers.md`).
- [ ] **16.** A few days later, post the forum announcement
      (`drafts/forum-post.md`) and add the thread link to the wiki page. The
      14-day window starts here.
- [ ] **17.** Set `[export] import_plan` in `config.toml` to the wiki URL
      (Claude can do this once the page exists).

## Phase 5 — Production, City only

- [ ] **18.** Day 15 or later, with no objection left unanswered: upload the
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
- [ ] **23.** Separate changesets, the FWFN tiles only.

## Phase 7 — Close and maintain

- [ ] **24.** Closing report on the wiki page and the forum thread.
- [ ] **25.** Add `[maintenance] since = "<date>"` to `config.toml` and copy the
      engine's `scripts/maintenance-reminder.caller.yml` to
      `.github/workflows/maintenance-reminder.yml`. From then on, a reminder
      issue arrives on the 1st of each month.
