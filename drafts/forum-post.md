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

*Thunder Bay is on the traditional lands of the Anishinaabe peoples, including Fort William First Nation, within the Robinson-Superior Treaty territory, and is part of the historic Métis homeland. First Nations should have more say in, and more ownership of, how their traditional lands beyond their reserves are developed, including the land Thunder Bay stands on.* (The first sentence adapts the City of Thunder Bay's
[Deepening Understanding](https://www.thunderbay.ca/city-hall/indigenous-relations/deepening-understanding/) page.)

**What and how much**
- The City publishes 45,102 address points. Against the 2026-11-06 Geofabrik
  extract, 44,379 City addresses are not in OSM (99%). What OSM has today is
  almost entirely CanVec 6.0 interpolation: 6,604 odd/even range ways, whose
  endpoints are 12,763 of the city's 12,950 address nodes.
- Create-only: new address nodes with `addr:housenumber`, `addr:street` and
  `addr:source`. No deletions, no edits to existing objects, no buildings.
  The CanVec ranges are left alone; retiring them is a later, separate
  effort, reviewed line by line through MapRoulette, with its own forum post.
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
lists as "Sq**w Bay Road"(!!!, even google map lists it like that)

**Questions where local input would help**
* Should nodes inside the city carry `addr:city=Thunder Bay`, or stay without
   it as in Toronto?

The review window is 14 days from today. Pilot first, then ward by ward. I'm
happy to take reviewers: if you map in Thunder Bay and want to look at a tile
before it goes up, reply here or write to toronto@comentality.com.

Thanks!
