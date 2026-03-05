# Combination Walkthrough Examples

These examples show how to go from an artistic idea to a concrete technique palette.

---

## Example 1: "I want something that feels like charcoal on rough paper"

**Step 1 — Identify the medium:** charcoal-conte

**Step 2 — Pull core techniques:**
- `fat-line-stroke` — broad gestural marks
- `stroke-hatching` — building up tone gradually
- `erode-dilate` — smudging and blending

**Step 3 — Add supporting techniques selectively:**
- `texture-synthesis` — paper grain that catches charcoal
- `ghost-stroke-doubling` — dust halo around marks

**Step 4 — Check for intent alignment:**
User wants "rough paper" → leans toward "raw, physical, handmade" intent.
Cross-referencing: `stroke-hatching`, `erode-dilate`, `texture-synthesis` all appear in both.
Good alignment.

**Step 5 — Final recommendation (4 techniques):**
1. **fat-line-stroke** (primary mark) — broad charcoal sweeps
2. **stroke-hatching** (tone building) — cross-hatch for darker areas
3. **erode-dilate** (material behavior) — smudge/blend passes
4. **texture-synthesis** (surface) — rough paper grain

**Unexpected suggestion:** Try `flow-fields` to guide the gestural sweep direction — charcoal strokes that follow an invisible force, like wind across the paper.

---

## Example 2: "Make it feel mysterious and deep, like fog"

**Step 1 — Identify the intent:** "mysterious atmospheric depth"

**Step 2 — Pull starting techniques:**
- `layered-composition` — depth through overlapping transparent layers
- `domain-warping` — organic, fog-like distortion
- `fbm-noise` — multi-scale cloud-like noise

**Step 3 — Add richness:**
- `gradient-systems` — smooth tonal transitions for atmospheric perspective
- `ghost-stroke-doubling` — spectral echoes add mystery

**Step 4 — Check the avoid list:**
Avoid `grid-layout`, `posterize-quantization`, `concentric-ring-fill` — these are too structured/graphic for fog.

**Step 5 — Check medium fit:**
This maps naturally to `watercolor-wash` — transparent layers, soft edges, bleeding.
Cross-reference with watercolor medium confirms: `flow-fields`, `blend-modes`, `gradient-systems` all align.

**Step 6 — Final recommendation (4 techniques):**
1. **layered-composition** (structure) — 3-5 depth layers, back to front
2. **domain-warping** (atmosphere) — warp coordinates for fog movement
3. **fbm-noise** (foundation) — multi-scale noise drives everything
4. **gradient-systems** (color) — soft transitions between warm/cool

**Unexpected suggestion:** Try `erode-dilate` at very low strength on each layer — fog doesn't have clean edges, everything should bleed slightly into its neighbors.

---

## Example 3: "I want geometric tiles but not boring"

**Step 1 — Identify the intent:** "structured but not rigid"

**Step 2 — Pull starting techniques:**
- `apparatus-grid` — irregular rectangular blocks (already less boring than pure grid)
- `recursive-subdivision` — nested structure at multiple scales
- `voronoi-tessellation` — organic cell division as an alternative to rectangles

**Step 3 — Add richness that breaks rigidity:**
- `warp-displacement` — bend the grid slightly so it breathes
- `noise-density-scatter` — vary content density across cells
- `cosine-gradient-palette` — rich color that shifts across the composition

**Step 4 — Check medium fit:**
Tiles suggest `woven-textile` or `ceramic-glaze`. Let's go ceramic:
- `domain-warping` (glaze pooling)
- `alpha-spatter` (mineral speckle)
- `voronoi-tessellation` (crackle)

Good overlap with our technique palette.

**Step 5 — Final recommendation (4 techniques):**
1. **apparatus-grid** (structure) — the Mondrian-like tile skeleton
2. **warp-displacement** (life) — subtle bending so nothing is perfectly straight
3. **cosine-gradient-palette** (color) — smooth color that shifts per tile
4. **voronoi-tessellation** (texture) — crackle pattern within tiles

**Unexpected suggestion:** Try `stroke-hatching` inside some tiles instead of flat fills — it turns geometric tiles into something that feels hand-printed, like risograph or letterpress.

---

## How to present recommendations

1. **Lead with the feeling**, not the technique names
2. **Limit to 3-5 techniques** — explain why each one is there
3. **Name the roles** — "primary mark", "structure", "surface", "color"
4. **Always include one surprise** — an unexpected combination that could lead somewhere new
5. **Mention what to avoid** — techniques that would fight the intended feel
