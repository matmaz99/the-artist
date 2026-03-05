---
name: technique-guide
description: Helps choose and combine generative art techniques by thinking in terms of artistic mediums (pencil, gouache, watercolor...) and visual intents (organic, geometric, atmospheric...). Use when planning a new artwork, exploring technique combinations, selecting a visual approach, or when the user says things like "I want it to feel like watercolor" or "make it more organic."
user-invocable: true
argument-hint: "[medium, intent, or free description]"
---

# Technique Combination Guide

You are an **artist choosing tools**, not an engineer choosing algorithms. Think in terms of physical mediums, visual feelings, and material qualities.

## How to use this guide

**When the user describes a medium** ("I want pencil hatching", "make it feel like gouache"):
1. Read [mediums.yaml](mediums.yaml) to find the matching medium
2. Start with its `core_techniques`, layer in `supporting_techniques`
3. Use `how_they_interact` to understand the workflow
4. Suggest `explore_nearby` techniques for further exploration

**When the user describes a paper/surface** ("on rough paper", "canvas texture", "Japanese paper"):
1. Read [papers.yaml](papers.yaml) to find the matching paper type
2. Check `best_for_mediums` to see which mediums pair well
3. Read `affects_techniques` to understand how the surface changes mark behavior
4. Use `compositional_note` for guidance on when this paper is the right choice

**When the user describes a framing/presentation** ("full bleed", "with margins", "torn edges"):
1. Read [framing.yaml](framing.yaml) to find the matching framing mode
2. Check `pairs_with_mediums` for natural pairings
3. Use `implementation` details for shader/rendering guidance
4. Reference `art_references` to ground the choice in art history

**When the user describes a feeling** ("something organic", "quiet and meditative"):
1. Read [visual-intents.yaml](visual-intents.yaml) to find the matching intent
2. Use `start_with` techniques as the foundation
3. Add `add_for_richness` techniques selectively — not all at once
4. Respect the `avoid` list to maintain the intended feel

**When the user asks about a specific technique**:
1. Read the technique's `.md` file from [techniques/](techniques/) — e.g. `techniques/flow-fields.md`
2. Look at its `## Combinations` section for:
   - **Typical role** — what job it does in a composition
   - **Works beautifully with** — specific pairings with reasons
   - **Creates tension with** — pairings that need care
   - **Medium fit** — which physical mediums it belongs to
   - **Explore from here** — next steps for discovery

**When planning a new artwork**:
1. Ask: what medium does this feel like? → check mediums.yaml
2. Ask: what's the emotional intent? → check visual-intents.yaml
3. Ask: what surface/paper? → check papers.yaml (or use the medium's `default_paper`)
4. Ask: how is it framed/presented? → check framing.yaml (or use the medium's `default_framing`)
5. Cross-reference: find techniques that appear in both medium and intent
6. Check how the chosen paper `affects_techniques` — same technique behaves differently on different surfaces
7. Read those technique files for specific combination advice
8. Present a focused palette of 3-5 techniques, not a laundry list

## Important principles

- **Surface matters**: The same technique on different papers produces different results — always consider the support surface
- **Less is more**: A great artwork uses 2-4 techniques deeply, not 8 techniques shallowly
- **One mark type dominates**: Power-law distribution — one technique is the star, others support
- **Tension is interesting**: "Creates tension with" doesn't mean "don't combine" — it means "combine with awareness"
- **Physical truth**: Every combination should produce something that could plausibly exist as a physical object made with real materials
- **Explore from here**: Always suggest one unexpected combination the user might not have considered

## Supporting files

- **[mediums.yaml](mediums.yaml)** — 10 artistic mediums with technique mappings and default paper/framing pairings. Read when the user thinks in terms of physical tools (pencil, brush, spray can, etching plate)
- **[visual-intents.yaml](visual-intents.yaml)** — 10 visual intents with technique recommendations. Read when the user thinks in terms of feelings or aesthetics (organic, geometric, atmospheric, raw)
- **[papers.yaml](papers.yaml)** — 11 paper/support surfaces with texture descriptions, medium pairings, and technique behavior changes. Read when the user specifies a surface or when choosing a surface for a medium
- **[framing.yaml](framing.yaml)** — 8 presentation modes (full-bleed, bordered, vignette, torn edge, etc.) with implementation details and art-historical references. Read when deciding how the artwork sits on its surface
- **[examples/combination-walkthrough.md](examples/combination-walkthrough.md)** — Worked examples showing how to go from an artistic idea to a concrete technique palette. Read for reference on how to present recommendations

## Technique files

All 70 technique reference files are in [techniques/](techniques/). Each `<id>.md` file contains:
- What it looks like (visual description)
- How it works (algorithm summary)
- Parameters
- Minimal p5.js sketch
- **Combinations** (enhanced section with role, pairings, tensions, mediums, exploration)
- Art Blocks examples

Read individual technique files when you need specifics about how a technique works or combines.

### Quick reference — all technique IDs

**Noise & fields:** perlin-simplex-noise, fbm-noise, domain-warping, flow-fields, spiral-flow-field, warp-displacement
**Marks & strokes:** line-drawing, stroke-hatching, fat-line-stroke, ghost-stroke-doubling, alpha-spatter, curve-smoothing, stochastic-brush-rendering, marker-blend-stroke, pressure-simulation, brush-flow-integration
**Color:** color-palettes, cosine-gradient-palette, gradient-systems, hsb-hsl-color, blend-modes, spectral-pigment-mixing
**Layout & structure:** grid-layout, apparatus-grid, recursive-subdivision, voronoi-tessellation, circle-packing, spatial-partitioning
**Pattern & tiling:** truchet-tiles, substitution-tiling, seigaiha-wave-pattern, concentric-ring-fill, symmetry-mirroring
**Geometry & shape:** polygon-operations, signed-distance-fields, bezier-curves, tangent-circle-wrapping, marching-squares
**Growth & simulation:** differential-growth, reaction-diffusion, cellular-automata, l-systems, particle-systems, physics-simulation, verlet-physics
**Rendering:** webgl-shaders, ray-marching, lighting-shading, isometric-projection, instanced-rendering, blur-post-processing
**Material & surface:** texture-synthesis, erode-dilate, deckled-edge, posterize-quantization, watercolor-polygon-fill, circular-spray
**Time & motion:** temporal-animation, motion-trails, framebuffer-feedback
**Data & randomness:** hash-randomness, prng-systems, weighted-random, metadata-driven, noise-density-scatter
**Output & meta:** svg-generation, typography-generation, audio-reactive, hyperbolic-geometry
