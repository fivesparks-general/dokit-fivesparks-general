+++
kind = "step"
created = 2026-11-19T19:47:12Z
state = "closed"
resolution = "done"
part_of = "solip-obeya:kv7z"
refs = [
  { doc = "dokit:DEC-115", role = "output" },
]
+++
# Former prefixes resolve: dokit 0.1.6 is installed

**Answer to `solip-obeya:kv7z`:** done as asked, and generalized. Dokit engine 0.1.6, `fivesparks-general/dokit@d3b6bc4c690e57e77d20825b522e1227ae28bf69` on `main`, is installed on the host with its skill and contract. The decision is `dokit:DEC-115`, "Every name keeps its history", and the exact rules are in the installed contract: §1, §3.1 (`prefix_formerly`), §5 (`formerly`) and §8.2.

**What a docket can now declare:**

- `[docket].prefix_formerly = { decision = ["ADR"] }` beside `prefix = { decision = "DEC" }`. After that, `ADR-123` and `solip-factory:ADR-123` name `DEC-123` in every field that names a doc (`refs`, `part_of`, `supersedes`). `brief`, the page and the export show the current id. The page's addresses, the ids it links in bodies, and the write verbs' `--part-of` and `--subject` all accept the former spelling.
- A doc's own `formerly = ["DEC-007"]`, for a doc renumbered or moved to another kind within its docket. You didn't ask for this; it uses the same mechanism.
- A reference resolves in the order docket's former name, then former prefix, then former id. So a citation spelled any way the name once was still resolves.

**Rules to plan the rename around:**

- **Old prefixes are reserved.** A former prefix that is a kind's current prefix, or that two kinds claim, is `docket.prefix-collision`. A former doc id that a doc has now, or that two docs claim, is `docs.former-conflict`. Both are errors.
- **One spelling on disk.** A file still named with a former prefix is `docs.former-prefix`, an error that names the file it should be. It is read under its current id, so a leftover file next to its renamed copy is also `ids.duplicate`.
- **Numbers are never reissued.** `dokit doc new` skips every number a doc once had.
- **A doc that moves to another docket is superseded, not renamed.** `formerly` takes local ids only. Write the new doc with `supersedes = "<old docket>:<old id>"` and leave the old one where it is. Supersedes across dockets resolve end to end, even through a renamed docket.
- **Engine bound.** A docket that declares `prefix_formerly`, or whose docs carry `formerly`, declares `engine = ">=0.1.6,<0.2"`.

**What this unblocks:** `PLAN-007` step 2.1. Renaming a prefix becomes one commit per docket:

1. `git mv` every file of the kind to the new prefix.
2. Set the new prefix under `prefix`.
3. Add the old one to `prefix_formerly`.
4. Raise `engine`.

No citation is touched. Once the renames land, `allocation.toml` can drop each grandfathered prefix it renamed.
