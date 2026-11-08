# Forum announcement — DRAFT, not posted

**Where:** OSM Community Forum → Communities → Canada
(<https://community.openstreetmap.org/c/communities/ca/>), tag `import`.
**When:** after the wiki page is live, the FWFN letter has gone out, and
Matthew Darwin and eireidium have had a few days with the direct note
(`drafts/local-mappers.md`).
**Title:** Thunder Bay address import: proposal for review

Replace each `{…}` before posting.

---

Hi all,

I'd like to propose an import of the civic addresses OSM is missing in
**Thunder Bay**, from the City of Thunder Bay's open address data. The full
plan is on the wiki: {wiki link}.

*Thunder Bay is built on the traditional territory of the Anishinabek,
including the Ojibwa of Fort William First Nation, signatory to the
Robinson-Superior Treaty of 1850, and we acknowledge the contributions of the
Métis peoples. (Wording from the City of Thunder Bay's
[land acknowledgement](https://www.thunderbay.ca/city-hall/history-heritage-and-records/history-of-thunder-bay/).)*

**What and how much**
- The City publishes 45,102 address points. After conflation against a fresh
  Geofabrik extract, about {MISSING} are not in OSM. Most of the city has no
  per-address data today beyond old CanVec nodes.
- Create-only: new address nodes with `addr:housenumber`, `addr:street` and
  `addr:source`. No deletions, no edits to existing objects, no buildings.
- Every run is reviewed by a person before upload. One tile per changeset,
  from the dedicated `skfd imports` account, tagged `import=yes` and with
  `import_plan`.
- It's the same tooling that imported Toronto's addresses this year
  ([wiki](https://wiki.openstreetmap.org/wiki/Toronto/Import/AddressPoints))
  and now maintains Guelph's.

**Fort William First Nation**
The City's data also includes 378 addresses on Fort William First Nation land.
They're a separate phase: I've written to the Nation's Lands & Governance
office, and none of them will be uploaded until FWFN has had the chance to
answer. If they'd rather not, they stay out. 84 of them are on a road the City
lists as "Squaw Bay Road"; that name won't be uploaded, and we'll use whatever
the Nation calls it.

**Questions where local input would help**
1. CanVec address nodes that match are left alone. Is a cleanup of them wanted
   later?
2. 14 City numbers look like `123-4` (a unit after a hyphen). Split them into
   `addr:unit`, upload them as they are, or skip them?
3. Should nodes inside the city carry `addr:city=Thunder Bay`, or stay without
   it as in Toronto?

The review window is 14 days from today. Pilot first, then ward by ward. I'm
happy to take reviewers: if you map in Thunder Bay and want to look at a tile
before it goes up, reply here or write to toronto@comentality.com.

Thanks!
