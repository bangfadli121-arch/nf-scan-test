# Segments — locations.wellsfargo.com (EN)

URL lists for `scan-segment.yml` (one URL per line). Generated 14 Nov 2026
from the Wells Fargo deep scan #3 artefacts:

- Source: `live.txt` of `locations.wellsfargo.com` (scan #3, dispatch
  14 Nov 2026 12:21–12:22 UTC) — 18,343 live URLs in total.
- Kept: only URLs whose host is `locations.wellsfargo.com` AND whose path
  is NOT under `/es/` (the Spanish mirror) — **7,038 URLs**.
- Excluded (deliberately, NOT scanned by these segments):
  - `/es/*` Spanish mirror on the same host — 7,023 URLs, same pages in
    Spanish; segment later as `es` segments if needed.
  - 4,282 live URLs on OTHER hosts found while crawling locations
    (e.g. `www.wellsfargo.com`, `dyn.mktgcdn.com`, `www.wellsfargojobs.com`).
    Those hosts are outside this segment plan; `dyn.mktgcdn.com` is not
    Wells Fargo infrastructure and must never be scanned.

## Segments (5, greedy-balanced by US-state path prefix, ~1,405 URLs each)

| Segment | URLs | States / paths |
|---|---|---|
| `locations-en-seg-01.txt` | 1,411 | ca |
| `locations-en-seg-02.txt` | 1,405 | tx, az, co, ut, nm, ne, wy, de, (root) |
| `locations-en-seg-03.txt` | 1,405 | fl, va, ny, md, id, sd, il, nd, mo, search |
| `locations-en-seg-04.txt` | 1,412 | nj, pa, sc, wa, nv, ct, wi, tn, ms, ks |
| `locations-en-seg-05.txt` | 1,405 | nc, ga, mn, or, al, ia, ak, mt, dc, ar, index.html |

Total: **7,038 URLs** (no overlap, no gaps; every URL verified
`locations.wellsfargo.com`, no `/es/`). Note: the plan mentioned 7,039 —
the actual EN count in `live.txt` is 7,038 (one fewer).

## How to add a segment

1. Put the URL list in this folder as `<name>.txt` (one URL per line,
   all under `*.wellsfargo.com` — the workflow scope guard rejects anything else).
2. Add the short name to the `segment` choice list in
   `.github/workflows/scan-segment.yml`.
3. Dispatch: `gh workflow run scan-segment.yml --ref main -f segment=<name> -f mode=deep`
