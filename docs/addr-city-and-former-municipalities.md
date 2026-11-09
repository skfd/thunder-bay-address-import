# `addr:city` and former municipalities: what Ontario actually tags

Survey of the Geofabrik Ontario extract dated 2026-11-07, run 2026-11-09 with
the engine's `scripts/addr_admin_tag_survey.py`, plus a full count of every
`addr:city` value by object type (1,982 distinct values). It backs the
proposal's "Not written: `addr:city`, `addr:province`" line and its open
question on `addr:city=Thunder Bay`.

## Thunder Bay itself

Thunder Bay is an amalgamated city too: Fort William, Port Arthur and the
townships of Neebing and McIntyre merged in 1970. Yet the old names have
vanished from OSM:

| `addr:city` | Count | Mostly on |
|---|---:|---|
| Thunder Bay | 12,638 | address nodes (12,395); 233 buildings |
| Oliver Paipoonge | 1,108 | address nodes (a separate municipality) |
| Shuniah | 428 | address nodes (a separate municipality) |
| Neebing | 413 | address nodes (today's separate municipality of that name) |
| Fort William First Nation | 10 | 8 buildings, 2 nodes |
| Kakabeka Falls, Rosslyn, Slate River, Gorham, Lappe, Hymers, Kaministiquia | 1–7 each | buildings |
| Fort William, Port Arthur, Westfort, Current River | **0** | — |

So unlike Hamilton, Sudbury or Toronto, Thunder Bay has a single convention
already: the current municipality, carried by the CanVec/StatCan layer. Rural
community names (Rosslyn, Slate River…) appear only on a handful of
hand-mapped buildings outside the city. Not writing `addr:city` adds no
conflicting value; writing `Thunder Bay` would match the existing layer but
add nothing a boundary does not already say. FWFN stays the Nation's call.

## Province-wide: three different things get called "city"

1. **The current, legal municipality:** Hamilton, Vaughan, Greater Sudbury,
   Chatham-Kent, Norfolk County.
2. **The former municipality** from before amalgamation: North York,
   Etobicoke, Stoney Creek, Nepean, Flamborough.
3. **The postal or local community**, never a municipality: Maple,
   Woodbridge, Waterdown, Chelmsford, Caledonia, Orléans.

The wiki defines `addr:city` as the postal city
([Key:addr:city](https://wiki.openstreetmap.org/wiki/Key:addr:city)), and
that is usually the third kind, sometimes the second, and only by chance the
first.

### Imports wrote the current municipality; hand mapping writes the community

| Current municipality | Count | Mostly on | Community names (mostly on buildings) |
|---|---:|---|---|
| Hamilton | 46,055 | address nodes (44.8k) | Ancaster 375, Waterdown 305, Stoney Creek 109, Carlisle 105, Dundas 100 |
| Vaughan | 17,815 | address nodes (16.6k) | Maple 3,810, Woodbridge 447, Concord 114 |
| Chatham-Kent | 22,765 | address nodes | Chatham 819, Blenheim 103, Wallaceburg 97 |
| Kawartha Lakes | 16,377 | address nodes | Lindsay 189, Bobcaygeon 65 |
| Norfolk County | 14,605 | address nodes | Simcoe 61, Waterford 29 |
| Haldimand County | 6,672 | address nodes | Caledonia 377, Dunnville 323 |

The split runs by source, not by place. "Norfolk County" and "Haldimand
County" are census names, not postal cities.

- **Toronto:** Toronto 209k; North York 8.4k, Etobicoke 3.8k, Scarborough
  2.4k, East York 1.7k, York 627, the former names mostly on buildings.
- **Greater Sudbury:** no convention. "Greater Sudbury" 13.0k (nodes),
  "Sudbury" 8.6k (almost all buildings), Chelmsford 336, Hanmer 263.
- **Ottawa:** barely tagged (its import wrote no city), and split even on
  spelling: Orleans 217, Orléans 170.
- **Mississauga:** clean (38k, Port Credit 1, Malton 1) because of a rename
  sweep.

### Traps

- **Former municipality ≠ postal community.** Hamilton's `COMMUNITY` field
  says "Flamborough"; mappers write "Waterdown" (305 to 7).
- **Communities straddle municipalities.** Thornhill (1,262) is half Vaughan,
  half Markham.
- **Ambiguous names.** "York" (former Toronto borough vs York Region);
  "Richmond" (Ottawa vs Richmond Hill).
- **Rename sweeps have happened twice** ("City of Hamilton → Hamilton", 9,750
  changes; "Municipality of Kincardine → Kincardine"), both toward the
  current-municipality convention, both leaving residue.

### The three choices for an import

- **(a) Write nothing.** Toronto's and this proposal's choice. Matches the
  wiki's "often redundant inside administrative boundaries"
  ([Addresses](https://wiki.openstreetmap.org/wiki/Addresses)); geocoders
  derive the city from boundaries.
- **(b) Write the current municipality.** Matches the CanVec/StatCan layer,
  but adds nothing the boundary does not already say.
- **(c) Write the postal community.** The only choice that adds information,
  and the one matching the wiki's definition, but it needs a source field
  that really is postal, and local agreement first.

Default to (a); (c) only with a postal source field and local agreement.
Canada Post's list of valid municipality names was not checked; it would
settle what "postal city" means place by place.

## `addr:province`, for the record

Province-wide, `addr:province` is on 0.6% of standalone address nodes, 0.17%
of interpolation end nodes and 6.4% of addressed buildings; the big imports
skip it, and every province has a boundary
([Key:addr:province](https://wiki.openstreetmap.org/wiki/Key:addr:province):
"this tag may be redundant there"). Where it is used, values go against the
wiki's `ON` recommendation: `Ontario` 37,767, `ON` 22,529, plus about 190 odd
casings.
