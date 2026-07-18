# CLAUDE.md — Casa Dos Hermanos

## What this is
Eight-page static site + data companions for a KB Home Plan 2088 build (Aurora, CO), co-owned by Salieri (upper floors) and Daniel (basement). Audience: family, on phones, via GitHub Pages. Governing constraint: **LOW EFFORT** — no frameworks, no build step, plain cross-linked HTML. This repo is the single source of truth. Never work from memory of a file; read it first.

## File map
- `index.html` — landing hub; cards HEAD-check their targets and auto-hide missing ones
- `brief.html` — design brief. Version badge appears in BOTH `<title>` and the `.brand` div — **bump both on any content edit** (currently v26)
- `plan.html` — interactive plan. Build marker = HTML comment after `</title>` (currently interactive_v9). Key consts: `DATA` (rooms), `SW` (finish legend), `FLAGS` (truth ledger), `ROUGHIN` (electrical overlay — must stay equal to `data/cdh_roughin_v2_1.json`)
- `studio.html` — selection ledger: 323 rows / 42 groups. **Writes** `localStorage cdh_selection_ledger_v2`. Also: flooring panel (`cdh_flooring_rates_v1`), LVP colourway picker (`cdh_lvp_colour_v1`), Finishes-reference tab (`PALETTE`/`PALIMG`)
- `network.html` — UniFi topology + rough-in order (N-1.0 rev 2.1)
- `combos.html` — tile explorer v2. **Reads** the ledger key (read-only); own state `cdh_combos_v1`. Carries `COLLECTIONS` (tile dataset — the SOURCE for studio's two Daltile pal-tab categories: regenerate them from here on any change), `AUTH` (bath geometry from D4/dims v3), `ROOMGEOM`
- `lighting.html` — lighting studio (self-contained SVG room plans, 2700 K)
- `walk.html` — pre-drywall Walk Sheet W-1.0 (site-visit checklist)
- `swatches/` — catalogue-extracted swatches, referenced by absolute raw.githubusercontent URLs with `onerror` hiding
- Photos live at repo **root** (historical convention — don't move them)
- `data/` — sources of record (below)

## Sources of record (`data/`)
- `2088_authoritative_dims_v3.json` — dimensions. Supersedes KB schedule estimates; plan + brief are reconciled to it
- `cdh_roughin_v2_1.json` — electrical order **$4,235** (data 2,064 / power 1,237 / light 934; 32 add + 6 verify — great-room drop = 2× placed singles as of v2.1). **Head-end = Bedroom 2 walk-in closet** (garage superseded 13/07/26)
- `flooring_ratebook.json` — provenance-tiered flooring pricing (tiers A quoted … D uncited)
- `project_state.json` — frozen chat-era state snapshot (historical reference)

Numbers shown on pages must match these files. When a source updates, **grep the whole repo for the old value** — facts historically live on multiple surfaces.

## Locked decisions — do not re-litigate
- Flooring: COREtec Bryan Crossing LVP main floor ($5,288) · Lake Mabel KB322 + 8 lb pad ALL upstairs incl. stairs (price TBD, quote -7 pending) · Marble Obsession tile wet areas ($2,546) · stairs stay carpet (2018602 not required)
- Primary bath: **2009097** shower in lieu of tub, includes solid-surface seat ($2,129) — studio default
- Kitchen: counter and backsplash are TWO independent picks; "with Full Splash" quartz codes live in the counter group; `BSP-INC` is the backsplash baseline
- Network head-end: Bedroom 2 walk-in closet ("tech closet")
- Design DNA: Organic Modern 50 / Japandi 30 / Dark Academia 20 · walnut primary, white oak secondary · matte black plumbing/door hardware, aged brass for lighting/decor only · 2700 K · **never grey / cool / gloss**

## Validation chain — run after EVERY html edit
1. Each `<script>` block → `node --check`
2. Tag balance: openers == closers for div/section/table/tr/td/script/style
3. Fact edited? → whole-repo grep for the **old** value (expect zero, or an intentional supersession note)
4. New image/swatch URL? → `curl -s -o /dev/null -w "%{http_code}"` expect 200 (post-push)
5. Bump the artifact's badge/marker; name the change in the commit message

**Two-surface rule:** brief facts appear in the inventory TABLE and the room CARDS — patch both, then stale-grep.

## Editing rules
- Surgical anchored edits; assert anchor uniqueness before replacing; never rebuild a file from memory
- One canonical dataset per fact; pages sharing data (combos ↔ studio tile collections) note their source
- Never resolve a conflict silently — surface it with a recommendation
- Experiments on branches; `main` is what the family sees (Pages deploys from it)
- When a decision lands, add it to **Locked decisions** above in the same commit

## Open items (short list)
Quote -7 Lake Mabel → enter figure in studio rate input · KB verify list = the 6 `"status":"verify"` items in `cdh_roughin_v2_1.json` → then confirm the order (pre-drywall clock) · EV outlet dropped from order — confirm rationale · guest render missing (404 by design in brief) · primarybed image version unconfirmed · day/night image toggle unbuilt (8 pairs) · 48/53 drawing-set pages outstanding · Design Studio: LVP colourway sample test (Wiltshire / Bedford / Bastion / Ravenswood / Canterbury) + carpet 120 vs 200 vs Natural Tan drawdown
