# Generative Art Pipeline

*A complete methodology for producing generative artworks — from artistic vision to rendered canvas. Designed to be used as a Claude agent skill.*

---

## Overview

This document describes a five-phase pipeline for creating generative artworks that have the **materiality and physicality of real art objects** — not digital illustrations, not procedural patterns, but things that look like they were made by human hands with physical materials.

The ultimate test for any output: **could this be a photograph of a real artwork?** If you showed the rendered canvas to someone and said "this is a photo of an oil painting / a collage / a watercolor / a screen print" — would they believe you? If the answer is no, the work isn't done. Every decision in this pipeline serves that goal.

**CRITICAL: Every artwork is unique.** The techniques, colors, composition strategies, and code architecture should be derived entirely from the vision spec — not recycled from previous artworks. An oil painting on linen demands completely different code than a Cubist paper collage, a Japanese woodblock print, a watercolor landscape, or a mixed-media assemblage. If you find yourself reusing code, techniques, or color palettes from a previous project, stop and ask: *does the spec actually call for this, or am I defaulting to what I know?*

The pipeline:

```
Phase 1: Vision Spec        (art-masterpiece-designer skill)
Phase 2: Technique Palette   (technique-guide skill)
Phase 3: Notebook Prototyping (isolated technique calibration)
Phase 4: Composition          (layer-based material interaction)
Phase 5: Iteration            (visual feedback loop with the user)
```

Each phase feeds into the next. **Skip none of them. Execute them in order.**

**CRITICAL: Do NOT skip Phase 3 (Notebooks).** The most common failure mode is reading technique files and jumping straight to composition. This always produces a bad painting on the first attempt, because you have no calibrated parameters. You MUST build isolated notebooks for each technique, iterate on each one (render → screenshot → verify against spec → fix → repeat), and only then begin composition. Phase 3 is where you learn what the techniques actually look like at your canvas size with your color palette. Without this, your composition will be guesswork.

**The non-negotiable rule:** The vision spec is the contract. Every render — whether notebook or composition — must be screenshotted and verified against the spec. If the spec says "deep Prussian blue darkness in the upper third," you open the screenshot, look at the upper third, and ask: *is this deep Prussian blue darkness?* If not, you iterate until it is. The painting is not done until every element described in the spec is visually present and convincing in the rendered output.

---

## Phase 1: Vision Spec

**Tool:** `art-masterpiece-designer` skill

**First action:** Create the project folder for this artwork (see *Project Setup & File Organization* below). The vision spec will be the first file written inside it.

Before writing any code, produce a **vision spec** — a detailed document describing the artwork as if briefing a master painter. This is the single source of truth for every decision that follows. Save it at the root of the project folder as `artwork_name_vision_spec.md`.

During the inspiration research (Phase 2 of the art-masterpiece-designer skill), **download reference images** of the master artworks that inspire this piece. Create a `references/` folder inside the project and save them there. These are the artist's studio wall — visual references you and the user can return to throughout the entire process. Name them clearly: `artist_name_-_title.jpg`.

### What the vision spec must contain

1. **Artistic roots** — which movements, which masters, which tensions between influences
2. **Composition** — format, spatial depth, tonal architecture, focal hierarchy
3. **Techniques** — specific studio techniques mapped to areas of the painting. Not "where" as a bounding box, but "where" as a natural consequence of the medium and gesture
4. **Physical materials** — describe the artwork in terms of real materials specific to its medium. Examples:
   - Oil painting: "Prussian blue oil glaze built up in 8 transparent layers over oxide red underpainting on Belgian linen with visible plain-weave thread"
   - Collage: "torn fragments of 1940s French newspaper on heavy grey cardboard, some pieces overlapping, edges showing paper layers and fibers"
   - Screen print: "three-color separation (cadmium red, ultramarine, black) on uncoated cream stock, 85 lpi halftone, 0.5mm registration drift between layers"
   - Charcoal: "compressed charcoal and vine charcoal on Ingres paper, heavy tooth visible in light passages, smudged transitions in mid-tones"

   The spec should make you feel the physical material — weight, roughness, wetness, opacity, fragility. If it reads like a description of a digital filter, rewrite it.
5. **Visual description** — precise, cinematic detail of what the viewer sees, including colors specified as pigment names with RGB values, not vague adjectives
6. **Hidden details** — elements that reward close inspection
7. **Rationale** — why every major choice serves the artistic intent

### Why the spec matters

The spec is what keeps you honest during composition. When you're debugging why a technique looks wrong, you go back to the spec and re-read how it's described. The spec's language tells you what the technique should *feel* like — and that feeling guides the implementation. Without the spec, you'll make engineering decisions instead of artistic ones.

The spec should be written in language an artist working in the chosen medium would understand. If it reads like a programming requirements doc, rewrite it.

### The spec as acceptance criteria

The vision spec is not a suggestion — it is the acceptance criteria for the final artwork. During composition (Phase 4) and iteration (Phase 5), you will constantly return to this document. For every render, you must:

1. **Screenshot the rendered canvas**
2. **Open the vision spec side by side**
3. **Walk through every described element** and ask: *is this visible? Does it match the description?*
4. **Log what's missing, what's wrong, what's close**
5. **Fix the most critical gap and render again**

If the spec says "calligraphic marks embedded in the dark passages, barely visible — the ghost of handwriting," then you look at the dark area of your render and ask: can I see calligraphic marks? Are they barely visible? Do they feel like a ghost of handwriting, or like garish lines? This is the level of fidelity required.

A composition that looks "pretty good" but misses elements from the spec is not done. A composition that includes all spec elements but doesn't match their described character is not done. The spec is the standard.

---

## Phase 2: Technique Palette

**Tool:** `technique-guide` skill

With the vision spec in hand, map each described technique to algorithmic building blocks.

### How to use the technique-guide

**Start fresh every time.** Do not carry over technique selections from previous artworks. Each artwork's technique palette must be derived from its own spec.

1. **Identify the medium.** Read `mediums.yaml` — the vision spec will describe something like "oil on linen," "paper collage on board," "three-color screen print," or "charcoal on rough paper." The medium determines which core techniques are available. **If the spec's medium doesn't match any entry in mediums.yaml closely, that's fine** — use the closest match as a starting point and adapt.

2. **Identify the visual intent.** Read `visual-intents.yaml` — the spec's artistic rationale maps to intents like "atmospheric," "organic," "raw," "geometric," "brutal." This narrows the technique palette further.

3. **Cross-reference.** Techniques that appear in both the medium and the intent are your strongest candidates. Read the individual technique `.md` files for each one to understand parameters, combination advice, and blend modes.

4. **Check the paper/surface.** Read `papers.yaml` — the support surface changes how techniques behave. Different surfaces produce fundamentally different results with the same technique.

5. **Produce a focused palette.** 3–8 techniques maximum. The roles depend on the medium:

   *For paint media:*
   - Primary brushwork, secondary texture, surface treatment, detail

   *For collage:*
   - Fragment generation/sourcing, placement logic, edge treatment, surface marks

   *For print media:*
   - Ink layer logic, halftone/pattern generation, registration system, paper surface

   *For drawing:*
   - Primary mark type, tonal building, erasure/highlight, smudge/blend

   **The role categories should match the medium.** Don't use painting roles for a collage.

### What the technique-guide doesn't tell you

The technique-guide gives you algorithmic primitives and combination advice. It does NOT tell you:
- How techniques interact when layered on a shared canvas (that's Phase 4)
- What parameter values produce a convincing result at your specific canvas size (that's Phase 3)
- How to compose multiple techniques into a unified painting (that's this methodology)

The technique-guide is a starting point. The notebooks and composition process are where the real craft happens.

**IMPORTANT:** Reading technique `.md` files is NOT the same as prototyping. You now know *what* the techniques are, but you have no idea what they *look like* with your specific colors and parameters. That's what Phase 3 is for. Do not skip to composition.

---

## Phase 3: Notebook Prototyping

**THIS PHASE IS MANDATORY. DO NOT SKIP IT.**

You may be tempted to jump straight to composition after selecting techniques. Do not. Every attempt to skip notebooks and go directly to composition has resulted in a bad painting that required more total iterations than if notebooks had been built first. The notebooks are not a formality — they are where you discover what each technique actually looks like with your specific colors, opacities, and blend modes at your canvas size.

**First action:** Create the `notebooks/` subfolder inside the project folder.

For each technique in your palette (typically 4–8 techniques), build an **isolated notebook** — a standalone HTML/p5.js sketch that develops that single technique to a convincing level. Save each notebook in the `notebooks/` subfolder. **Each notebook must go through its own iteration cycle: render → screenshot → verify against the vision spec's description of that technique → fix → repeat.** A notebook is accepted only when it visually matches what the spec describes.

### Why notebooks matter

Notebooks let you calibrate parameters in isolation. When you try to calibrate 8 techniques simultaneously in a composition, changing one parameter shifts everything else. Notebooks give you:

1. **Verified parameters** — opacity ranges, color values, blend modes, stroke counts that produce convincing results
2. **Algorithm clarity** — the core algorithm for each technique, debugged and understood before integration
3. **Visual reference** — what the technique should look like when it's working. This is your benchmark during composition.
4. **Iteration speed** — a notebook renders in seconds. A full composition takes minutes. Iterate on the notebook, integrate once into the composition.

### How to build a notebook

Each notebook should:

1. **Simulate the surface state** it will encounter in the composition. If the technique will be applied over a dark ground, start the notebook with a dark ground, not a white canvas. The surface state determines everything — a technique calibrated on white won't look the same on dark.

2. **Use the exact same blend mode** you'll use in the composition. The notebook's rendering approach must match what the composition will use.

3. **Run at a similar scale** to the composition. A technique that looks good at 400×400 may produce completely different results at 720×960.

4. **Be creative about implementation.** The technique-guide gives you algorithmic primitives, but don't limit yourself to purely procedural approaches. Think about what would produce the most convincing result:
   - If the spec calls for **newspaper collage**, don't just simulate newsprint with noise — fetch real vintage newspaper images from the internet, crop fragments, and composite them onto the canvas. The real thing will always look better than a simulation.
   - If the spec calls for a **handwritten letter texture**, find a real handwriting sample image and use it as a source texture, not a procedurally generated approximation.
   - If the spec calls for **photographic transfer**, use an actual photograph blended into the surface.
   - If the spec calls for **wood grain** or **marble**, a real texture image masked and blended will be more convincing than fbm noise trying to approximate it.

   The question to ask is: *what would a real artist do?* A real artist making a collage walks to a newsstand, buys old papers, and tears them. The digital equivalent is fetching real images and compositing them. A real artist making an oil painting mixes real pigments. The digital equivalent is subtractive pigment mixing math. Match the implementation to the medium — don't default to the same procedural toolkit for every artwork.

5. **Iterate freely.** There is no cost to versioning notebooks. Create v1, v2, v3... Each version refines the parameters. Accept a notebook only when it produces a result you'd be proud to show in isolation.

6. **Verify against the spec.** Every notebook iteration should be rendered, screenshotted, and compared to the vision spec's description of that technique. If the spec describes a specific visual quality, your notebook must achieve it. If it doesn't, you're not done iterating.

7. **Verify physicality.** Look at the notebook render and ask: does this look like it was made with real materials? Or does it look like a computer graphic? If the technique is supposed to be oil paint, does it feel like oil paint — with thickness, transparency variation, brush marks? If it's supposed to be torn paper, do the edges look torn — irregular, fibrous, with visible paper layers? If a technique looks "digital" in the notebook, it will look digital in the composition too. Fix it here, where iteration is cheap.

### What notebooks DON'T give you

Notebooks prototype techniques in isolation. The thing they cannot teach you is how techniques interact when layered. That's the critical gap, and it's what Phase 4 addresses.

**Honest assessment from practice:** Notebooks are most valuable for techniques that have complex standalone behavior — things with many parameters to tune (blend opacities, color mixing, edge profiles, stroke counts). They are less useful for techniques that are fundamentally relational — effects that only make sense in the context of what's already on the canvas (e.g., blending between two layers, veils that respond to color temperature). For those relational techniques, you're better off calibrating directly in the composition.

### Notebook-to-composition transfer

When you finish notebooks, extract these key values for each:

- **Color palette** — exact RGB values that work
- **Opacity ranges** — the working range for this technique on its expected surface
- **Blend mode** — multiply, pigment mix, additive, etc.
- **Density/count** — how many strokes, how many layers, how many passes
- **Core algorithm** — the essential math (the coverage function, the falloff curve, the noise frequency)

These become input parameters for Phase 4. But they will need adaptation — the composition surface is different from the notebook surface, even if you tried to match them.

### Gate: Before moving to Phase 4

**Do not begin composition until you have:**

- [ ] At least one accepted notebook for each major technique in your palette (typically 4–6 notebooks)
- [ ] Each notebook has been rendered, screenshotted, and verified against the spec
- [ ] Extracted key parameters (colors, opacities, blend modes, counts, algorithms) from each accepted notebook
- [ ] Shown the notebooks to the user and gotten confirmation they look right

If you have not done all of the above, you are not ready for composition. Go back and build the missing notebooks.

---

## Phase 4: Composition

This is where the painting is actually built. It is the hardest phase and the one most likely to go wrong.

**First action:** Create the `canvas/` subfolder inside the project folder. Each composition iteration will be saved here as a new versioned file (`artwork_name_v1.html`, `artwork_name_v2.html`, etc.).

**Before writing composition code, re-read the entire vision spec.** Not a skim — a careful, line-by-line reading. Internalize what the painting should look like. Then, as you build each layer, keep the spec open and verify that each layer's contribution moves the painting toward the described vision. After implementing the full layer stack, immediately render, screenshot, and compare against the spec. This is not optional — it is the core of the process.

### The Core Principle

**Make art like an artist, not like a programmer.**

You are simulating a physical process — but *which* physical process depends entirely on the spec. A painter loads a brush with pigment and drags it across canvas. A printmaker carves into a plate, inks it, and presses paper against it. A collagist cuts paper, arranges fragments, and glues them down. A weaver interlaces threads on a loom. Each medium has its own logic, its own accidents, its own physics.

Your code must think like the artist who works in *that specific medium*. Not "draw a blue rectangle at y < 300" but rather: how would this material actually behave? How does it interact with the surface? What does the artist's hand do?

**What makes digital art look digital:**
- Perfect gradients with no texture variation
- Uniform noise applied like a Photoshop filter
- Clean mathematical edges where real materials would bleed, feather, or break
- Flat color fills where real materials would have thickness or density variation
- Symmetry and regularity — real materials are always slightly uneven
- No visible support surface — real art is always *on* something
- Colors that glow from screen light instead of feeling like pigment, ink, dye, or paper
- **Same techniques appearing in every artwork regardless of medium** — this is the biggest giveaway

**What makes art feel physical (varies by medium):**

| Medium | Physical qualities to simulate |
|--------|-------------------------------|
| Oil painting | Surface weave visible through thin areas, paint thickness variation, brush gesture, slow drying allows blending |
| Watercolor | Paper grain, pigment granulation, wet bleeding edges, dry-brush skip, white of paper as lightest value |
| Collage | Cut/torn paper edges, overlapping opaque fragments, visible glue stains, different paper textures/colors |
| Screen print / risograph | Halftone dots, ink layer registration offset, flat color planes, overprint where colors overlap |
| Woodblock / linocut | Carved line texture, ink catch on wood grain, paper fiber impression, slight misregistration |
| Charcoal / conte | Paper tooth catching pigment, smudge areas, erased ghosts, dust scatter, finger marks |
| Etching / engraving | Plate tone, incised line character, ink pooling in grooves, embossed plate edge |
| Mosaic / ceramic | Grout lines between tesserae, color variation within tiles, irregular edges, surface sheen |
| Textile / weaving | Thread intersection texture, color mixing through interlace, selvage edges, slight warp |
| Photography / photomontage | Film grain, depth of field, exposure variation, cut edges in montage, darkroom artifacts |

**Choose the physical qualities that match YOUR artwork's medium.** Don't simulate oil paint characteristics for a collage. Don't add canvas weave to a screen print.

An artist doesn't have zone-gating functions. They build the work through the process natural to their medium, and the "regions" emerge from how materials accumulate and interact.

### The Anti-Pattern: Zone Gating

The naive approach to composing a multi-technique painting:

```javascript
// BAD: Zone-gated approach
let glazeStrength = smoothstep(y, zoneEdge, zoneEdge - transition);
let scumbleStrength = smoothstep(y, zone2Start, zone2End);
let soakStrength = smoothstep(y, zone3Start, zone3End);
```

**Why it fails:**
1. **Segmented result** — the painting looks like 3 separate paintings stitched together
2. **Artificial boundaries** — even with smoothstep, transitions feel programmed
3. **No interaction** — techniques don't respond to what's already on the canvas
4. **Parameter mismatch** — technique parameters calibrated in notebooks don't produce the same result when gated to a fraction of the canvas
5. **Not how real materials work** — real materials interact with the surface state

**Zone-thinking in disguise:** Even without `smoothstep`, if your code says "apply this technique only in the lower 30%," that's still zone-gating. The symptom is the same — artificial segmentation.

### The Approach: Layer-Based Material Interaction

#### Step 1: Establish the Layer Stack — From the Spec, Not a Template

Read the vision spec and extract the **process order** — the sequence an artist working in this medium would actually follow. This is chronological, not spatial: *what goes down first?*

**Do NOT use a fixed template.** The layer stack is different for every artwork because every medium has a different physical process. Derive yours from the spec.

**Examples of how different media produce different layer stacks:**

*Oil painting:*
```
1. Linen surface  2. Toned ground  3. Underpainting (thin wash)
4. Opaque passages (impasto)  5. Glazes (transparent layers)
6. Detail marks  7. Varnish
```

*Paper collage:*
```
1. Background paper/board  2. Large base fragments (glued flat)
3. Medium fragments (overlapping, angled)  4. Small detail pieces
5. Drawn/painted marks on top  6. Edge treatments
```

*Screen print:*
```
1. Paper surface  2. First ink layer (largest flat shape)
3. Second ink layer (overprints first)  4. Third ink layer
5. Registration artifacts between layers
```

*Watercolor:*
```
1. Paper surface (white — never fully covered)  2. Lightest washes
3. Mid-tone washes (wet-on-dry)  4. Detail (wet-on-wet for bleeds, dry brush for texture)
5. Darkest accents (final marks)
```

*Charcoal drawing:*
```
1. Paper surface  2. Broad tone laid with side of stick
3. Compressed charcoal for darks  4. Erasing for highlights
5. Fine marks for detail  6. Fixative spray (changes surface slightly)
```

**Key insight:** Each layer covers a broad area (often the whole canvas), but its visual effect at any pixel depends on what's already there. The layer stack must reflect the physical process of the specific medium — not a generic painting recipe.

#### Step 2: Define Spatial Strategy (Not Zone Gates)

Each layer needs a **spatial logic** — how its material distributes across the canvas. This is NOT a fixed formula. Derive it from how the actual medium behaves.

**Different media have different spatial logics:**

| Medium | Natural spatial distribution |
|--------|----------------------------|
| Oil painting | Coverage maps — layers accumulate from broad to narrow, building depth |
| Watercolor | Gravity-driven — washes pool at bottom, flow downward, paper stays white at highlights |
| Collage | Placement-based — fragments positioned explicitly, overlapping creates depth |
| Screen print | Full-coverage layers — each ink layer covers its whole stencil area, overprint creates new colors |
| Charcoal | Pressure maps — density follows hand pressure, eraser carves back to paper |
| Mosaic | Grid-based — tesserae fill a defined area, grout creates separation |
| Spray paint | Falloff gradient — dense at center of spray, dissipating outward in a cone |

**The principle is always the same:** spatial distribution should emerge from the medium's physics, not from arbitrary code boundaries. If you're writing `if (y > H * 0.6)` to confine a technique, you're zone-gating. Instead, ask: *why would this material end up here and not there?*

For paint-like media, **coverage maps** work well — each layer reaches a different extent across the canvas, with organic (noise-driven) boundaries:

```javascript
// Example for layered paint: each layer reaches a different extent
let boundaryY = H * reach[layerIndex];
let noiseOffset = fbm(x * freq + layer * 37, y * freq + layer * 53) * H * 0.05;
let actualBoundary = boundaryY + noiseOffset;
```

For collage, **explicit placement** is more natural — fragments go where the artist decides, with slight randomness in angle and position. For print media, **full-layer coverage** with overprint logic is the right model.

**The "zones" in the final artwork emerge from accumulation and process** — not from boundaries in the code.

#### Step 3: Material Interaction

This is the central innovation. Each technique checks the **current surface state** before applying its effect.

**The surface state is simply what the pixel looks like right now** — primarily its brightness, but also color temperature or any other property relevant to the technique.

```javascript
// Generic material interaction pattern:
let brightness = (pixels[idx] + pixels[idx+1] + pixels[idx+2]) / 3;
let surfaceResponse = map(brightness, darkThreshold, lightThreshold, minEffect, maxEffect);
let effectiveOpacity = baseOpacity * surfaceResponse;
```

**Material interactions vary by medium.** Here are examples across different media — use only what's relevant to YOUR artwork, and invent new ones as needed:

**Paint media:**
| Technique | Surface reads | Behavior |
|-----------|--------------|----------|
| Wash / stain | Brightness | Light surface absorbs fully, painted surface resists |
| Opaque stroke | Brightness | Shows on lighter surfaces, less visible on dark |
| Transparent glaze | Brightness | Darkens through multiplication, more dramatic over light areas |
| Dry brush | Surface texture | Catches on weave peaks, skips valleys |

**Collage / paper media:**
| Technique | Surface reads | Behavior |
|-----------|--------------|----------|
| Paper fragment | Position + overlap count | Placed by artist decision, later fragments cover earlier ones |
| Torn edge | Fragment boundary | Reveals layer beneath along irregular tear line |
| Glue bleed | Fragment edges | Slight darkening/sheen extending beyond fragment boundary |
| Pencil mark over collage | Surface color | Darker on light paper, invisible on dark fragments |

**Print media:**
| Technique | Surface reads | Behavior |
|-----------|--------------|----------|
| Ink layer | Previous ink presence | Overprint creates new color; uninked areas stay previous state |
| Halftone | Tonal value | Dot size maps to desired darkness — more dots = darker |
| Registration error | Layer index | Each successive layer drifts slightly from intended position |

**Drawing media:**
| Technique | Surface reads | Behavior |
|-----------|--------------|----------|
| Charcoal stroke | Paper tooth (texture) | Catches on rough grain, skips smooth areas |
| Eraser | Current darkness | Partially lifts mark back toward paper white |
| Smudge | Surrounding values | Blurs/spreads existing marks into neighboring areas |

The principle is always the same: **the technique reads the current surface and responds to it physically.** But *what* it reads and *how* it responds depends entirely on the medium.

**Result:** Each technique naturally concentrates where it makes physical sense, without any explicit zone boundary.

#### Step 4: Probability Distribution for Discrete Elements

For discrete elements (strokes, marks, dots), use **Gaussian probability distributions** centered where the spec says the technique should concentrate:

```javascript
let cx = gaussianRandom(centerX, sigmaX);
let cy = gaussianRandom(centerY, sigmaY);
```

This means:
- ~68% of marks land within 1σ of center (the "core zone")
- ~95% within 2σ (extending into neighboring areas)
- A few outliers appear anywhere — exactly like a real painter's strokes

No hard boundaries. No smoothstep. Just natural probability.

#### Step 5: Two-Pass Techniques

Some techniques need both **atmospheric** and **textural** components:

- **Pass A (pixel-level):** Creates the broad color/value shift visible from across the room — applied per-pixel with material interaction
- **Pass B (discrete marks):** Creates the visible texture/brushwork seen up close — p5.js strokes at low alpha

This mirrors how real art works at different viewing distances. Not every technique needs two passes — but any technique that should read both "from across the room" and "up close" does.

### Blend Modes

Use the physically correct blend mode for the materials in YOUR artwork. Different media demand different blending:

**Paint-like media (oil, acrylic, gouache):**
| Material | Blend mode | Formula |
|----------|-----------|---------|
| Transparent glazes | Multiply | `result = lerp(base, (base/255) * glaze, opacity)` |
| Opaque paint | Subtractive pigment mix | `sqrt(lerp(base², pigment², alpha))` * 255 |
| Thin washes | Subtractive at low alpha | Same formula, alpha < 0.3 |

**Ink-based media (screen print, risograph, letterpress):**
| Material | Blend mode | Formula |
|----------|-----------|---------|
| Opaque ink layer | Replace | Ink covers what's beneath (no mixing) |
| Overprint (ink on ink) | Multiply or darken | Colors mix subtractively where layers overlap |
| Halftone dot | Binary threshold | Dot is either ink or paper — no gradient |

**Collage / paper:**
| Material | Blend mode | Formula |
|----------|-----------|---------|
| Opaque paper fragment | Replace (with torn-edge alpha) | Fragment fully covers base, except at torn edges |
| Translucent tissue/vellum | Alpha composite | Base shows through tinted by overlay color |
| Glue stain | Slight darkening | Subtle multiply at very low opacity |

**Drawing media (charcoal, pencil, conte):**
| Material | Blend mode | Formula |
|----------|-----------|---------|
| Dry mark on paper | Darken only | Mark can only darken, never lighten (except erasing) |
| Eraser | Lighten toward paper | Partially restores paper color |
| Smudge | Blur + spread | Averages nearby values, spreads mark |

**Choose the table that matches your medium.** Don't use oil paint formulas for a collage. Don't use collage logic for a watercolor.

### Resolution Independence

Use a scale factor `S` so you can iterate at low resolution and render at high resolution:

```javascript
const S = 1;  // 1=draft (720×960), 3=hi-res (2160×2880)
const W = 720 * S, H = 960 * S;
```

**Scaling rules:**
- Positions expressed as fractions of W/H → auto-scale (e.g., `W * 0.42`)
- Absolute pixel values → multiply by S (e.g., `strokeWeight(2 * S)`, `blurRadius = 12 * S`)
- Noise frequencies → divide by S (e.g., `noise(x * 0.008 / S)`) to maintain same visual pattern size
- Opacity, color values → no scaling needed

Iterate at S=1 (fast, seconds to render). Deliver at S=3 (slow, but 9× more detail).

---

## Phase 5: Iteration

The composition will not be right on the first render. Expect 5–15 iterations. **This phase is not a polish step — it is where the painting actually comes together.** Most of your time should be spent here.

### The spec-verification loop

Every single iteration follows this exact sequence:

1. **Render** the canvas at S=1 (fast, a few seconds)
2. **Screenshot** the rendered output
3. **Analyze the screenshot against the vision spec.** Go through the spec element by element. For each technique or visual element described in the spec, ask:
   - Is it visible in the render?
   - Does it match the described character? (e.g., "barely visible" vs. prominent; "torn edges" vs. clean cuts; "deep darkness" vs. muddy grey)
   - Does it interact correctly with its neighbors? (e.g., a wash should bloom on raw surface but resist painted areas)
   - Does the overall color, mood, and spatial structure match the spec?
   - **Does it look physical?** Could you believe this was made with the real materials described in the spec? Or does it look like a computer made it? Check for the physical qualities specific to the artwork's medium (see the medium table in Phase 4). If anything looks like a Photoshop gradient, a uniform noise filter, or a clean geometric shape that the medium wouldn't produce — it needs more physicality.
4. **Identify the single worst discrepancy** between the render and the spec — not all problems, just the one that most breaks the painting
5. **Fix that one thing** in the code
6. **Render again and re-verify against the spec**
7. **Repeat until every element in the spec is present and convincing**

**Do not declare the composition done based on your impression.** Verify against the spec. If the spec describes 6 techniques and you can only identify 4 in the render, there are 2 missing. Find out why and fix them.

### When the user provides feedback

The user's visual feedback is the highest-priority signal. When the user screenshots a section and says "the linen texture is too coarse" or "I don't see enough warmth in the transition," that becomes the next iteration target. But even between user feedback rounds, you should be self-verifying against the spec — don't wait for the user to notice that calligraphic marks are missing.

### Common problems and their real causes

| Symptom | Likely cause | Fix |
|---------|-------------|-----|
| Painting looks segmented into bands | Zone-gating (explicit or disguised) | Replace with coverage maps + material interaction |
| Technique is invisible in the composition | Surface state doesn't match notebook | Check what the surface brightness/color actually is at that point; adjust technique parameters |
| Garish colored marks on dark surface | Alpha too high for discrete marks | Reduce alpha; use atmospheric wash for the broad color effect instead |
| Regular grid-like pattern visible | Using structural grid to gate effects | Remove structural gating; use pure Gaussian/noise for variation |
| One technique bleeding into wrong area | No material interaction on that pass | Add surface-state check so the technique responds to what's already there |
| Technique looks different from notebook | Different surface state in composition | Match the surface state to what the notebook assumed |
| Surface texture too coarse or too fine | Wrong scale for canvas size | Adjust texture period relative to canvas dimensions |
| Transitions between techniques feel artificial | Position-based boundaries | Let material interaction do the work instead of position checks |
| Everything looks procedurally generated | Over-reliance on noise for everything | Consider using real source imagery (textures, photos, found material) where the artwork calls for it |
| Artwork looks "digital" / too clean | Missing physicality: no surface texture, perfect edges, uniform gradients | Add medium-specific imperfections: surface visibility, imperfect edges, process artifacts |
| Colors glow instead of feeling like material | Using wrong color model for the medium | Paint: subtractive pigment mix. Print: multiply for overprint. Collage: no mixing. Drawing: darken-only. Match the medium. |
| **Every artwork looks similar** | **Reusing code architecture, techniques, or palettes from previous projects** | **Start from scratch. Derive layer stack, blend modes, spatial strategy, and color palette entirely from the new spec. Different medium = different code.** |

### When to go back to notebooks

If a technique is fundamentally not working in the composition, don't try to debug it there. Go back to the notebook, create a new version that better simulates the surface state it encounters in the composition, recalibrate, then re-integrate.

---

## Project Setup & File Organization

### Kickoff: creating the project folder

The very first action when starting a new artwork is to create its project folder. Everything lives inside this folder — spec, notebooks, composition files. The folder name should be the artwork title in a filesystem-friendly format (lowercase, hyphens or underscores).

```bash
# At kickoff, before any creative work begins:
mkdir -p "Artwork-Name"
```

### Phase 1 creates the spec file and references folder

The vision spec is the first file created inside the project folder. It is written directly at the root of the project — not in a subfolder. During the inspiration research, create a `references/` subfolder and download reference images of master artworks into it.

```bash
# Phase 1 output:
Artwork-Name/
├── artwork_name_vision_spec.md    # The vision spec (source of truth)
└── references/                     # Downloaded images of inspiring artworks
    ├── rothko_-_no_14.jpg
    ├── braque_-_violin_and_candlestick.jpg
    └── ...
```

### Phase 3 creates the notebooks folder

When you begin notebook prototyping, create the `notebooks/` subfolder. Each notebook is a standalone HTML file. Version freely — never overwrite, always create a new version file.

```bash
# Phase 3 — create on first notebook:
mkdir -p "Artwork-Name/notebooks"
```

Naming convention: `NN_technique_name.html` for v1, `NN_technique_name_vN.html` for subsequent versions. Number notebooks in the order they correspond to the layer stack (01 = support surface, 02 = primary technique, etc.).

### Phase 4 creates the canvas folder

When you begin composition, create the `canvas/` subfolder. This holds the full composition files — each iteration is a new version. Never overwrite a previous version; always create a new file.

```bash
# Phase 4 — create on first composition attempt:
mkdir -p "Artwork-Name/canvas"
```

### Full project structure

After all phases, the project folder looks like this:

```
Artwork-Name/
├── artwork_name_vision_spec.md           # Phase 1: the source of truth
├── references/                            # Phase 1: downloaded inspiration images
│   ├── rothko_-_no_14.jpg
│   ├── frankenthaler_-_mountains_and_sea.jpg
│   └── ...
├── assets/                                # (if needed) real images, textures, found material
│   ├── newspaper_fragment_01.jpg
│   ├── vintage_texture.png
│   └── ...
├── notebooks/                             # Phase 3: technique prototypes
│   ├── 01_support_surface.html
│   ├── 01_support_surface_v2.html
│   ├── 02_primary_technique.html
│   ├── 02_primary_technique_v2.html
│   ├── 02_primary_technique_v3.html      # iterate freely
│   ├── 03_secondary_technique.html
│   ├── 04_detail_technique.html
│   ├── ...
│   └── 05_edge_treatment_v2.html
├── canvas/                                # Phase 4-5: composition iterations
│   ├── artwork_name_v1.html              # first attempt (keep it)
│   ├── artwork_name_v2.html              # second attempt (keep it)
│   ├── artwork_name_v3.html
│   ├── ...
│   └── artwork_name_v8.html              # current best
└── notes.md                               # lessons learned (optional)
```

**Note the `assets/` folder.** If your artwork uses real source material (photographs, textures, found imagery, fonts), store them here. Not every artwork needs this folder — purely procedural paintings won't. But if the spec calls for collage, photographic transfer, real textures, or any non-procedural element, create this folder and populate it during Phase 3.

### Key rules

- **Never delete previous versions.** Versions are cheap. Being able to compare v3 vs v6 is invaluable when debugging regressions.
- **The spec lives at the root.** It's the first thing you see when you open the project. It's the document you open side-by-side with every render.
- **Notebooks and canvas are separate.** Notebooks are isolated experiments. Canvas files are full compositions. Don't mix them.
- **Version numbers in canvas files track iteration.** Each render → screenshot → analyze → fix cycle produces a new version. If you're on v6, that means you've done 6 cycles of spec verification.

### The HTML/p5.js Canvas File Structure

```javascript
const S = 1;  // Scale factor
const W = baseWidth * S, H = baseHeight * S;
const SEED = 42;  // Deterministic randomness

// Utility functions — choose based on your medium:
// Paint: fbm, pigMix (subtractive pigment blend), seeded RNG
// Print: halftone pattern, overprint blend, registration offset
// Collage: image loading, edge detection for torn/cut edges, fragment placement
// Drawing: pressure curves, smudge kernel, eraser blend

function setup() {
  createCanvas(W, H);
  pixelDensity(1);
  noLoop();
}

function draw() {
  background(...supportColor);

  // Layer functions derived from YOUR spec's process order.
  // These names are EXAMPLES — rename to match your actual techniques.
  // An oil painting might have: layerLinen, layerGround, layerGlaze, ...
  // A collage might have: layerBackground, layerBaseFragments, layerOverlap, ...
  // A screen print might have: layerPaper, layerInk1, layerInk2, layerInk3, ...

  // Each layer function:
  // 1. loadPixels()
  // 2. Read surface state at each pixel
  // 3. Apply technique with interaction appropriate to the medium
  // 4. updatePixels()
}
```

**The layer function names, count, and logic should be entirely different for each artwork.** If your `draw()` function looks the same as a previous project, you're not designing from the spec.

---

## Summary: The Mental Model

Think of the canvas as a physical object made with real materials. At every pixel, ask: *what material is here, and what would happen if I applied the next material on top of it?*

The answer depends entirely on the medium:
- **Oil paint** on oil paint → layers interact through transparency, impasto, and drying time
- **Paper** on paper → later fragment covers earlier fragment, except at torn edges
- **Ink** on ink → overprint creates a third color; uninked areas unchanged
- **Charcoal** on charcoal → builds up, can be erased/smudged, limited by paper tooth saturation
- **Watercolor** on dry watercolor → hard edge where wet meets dry; wet-on-wet → soft bleeding

**The regions in the final artwork are emergent** — they arise from the accumulation of layers and the physics of the medium, not from boundaries in the code.

### Every artwork must be different

This methodology gives you a **process** (5 phases, layer-based composition, material interaction). It does NOT prescribe a **style, medium, technique set, or color palette**. Those come from the vision spec — and the vision spec is different for every artwork.

**Signs you're falling into repetition:**
- Reusing blend mode formulas from a previous project without checking if they fit the new medium
- Defaulting to `fbm noise` for every texture (real art has many texture sources: weave, grain, tooth, halftone, crackle, each computed differently)
- Using the same color mixing approach (subtractive pigment mix) for media that don't involve pigment mixing (collage, print, photography)
- Writing layer functions with the same names/roles as a previous project
- Starting with linen texture + ground wash when the spec calls for a completely different surface
- Using the same 3-5 techniques from the technique-guide for every artwork

**What to do instead:**
- Read the spec fresh. What medium is this? What materials? What surface?
- Go to the technique-guide with *this specific artwork's* needs. Don't browse — search for what the spec demands
- Let the spec's medium dictate the code architecture. A collage has no "underpainting layer." A screen print has no "sfumato blending." An etching has no "soak-stain wash."
- Use real source material when the artwork calls for it: photographs, textures, found imagery, real fonts, scanned objects
- Invent techniques that aren't in the guide if the spec demands something novel

The technique-guide gives you 70+ algorithmic building blocks. But for some artworks, the right "technique" isn't in the guide — it's an image fetched from the internet, a font rendered to canvas, or a creative hack you invent. The guide is a starting point, not a cage.

---

## Anti-Patterns Checklist

Before considering a composition complete, verify you haven't fallen into these traps:

### Spec compliance (verify by screenshotting the render)

- [ ] **Every technique in the spec is visually present** — screenshot the render and check each one
- [ ] **Every technique matches its described character** — not just present, but *convincing* (e.g., "barely visible calligraphic marks" means barely visible, not invisible AND not prominent)
- [ ] **Color relationships match the spec** — if the spec says "Prussian blue darkness," it shouldn't be grey-brown
- [ ] **Spatial relationships match the spec** — if the spec says "warmth concentrates left of center into a vertical passage roughly the height of a human torso," verify the warm passage is there, is left of center, and is roughly torso-proportioned
- [ ] **Hidden details are present** — if the spec describes elements that reward close inspection, screenshot close-ups to verify they're visible at inspection distance
- [ ] **Overall impression matches the spec's artistic rationale** — step back from the pixel-level and ask: does this painting produce the emotional experience the spec describes?

### Physicality (the "could this be a photograph of a real artwork?" test)

- [ ] **Support surface is visible** — the underlying surface shows through where appropriate for the medium
- [ ] **No perfect gradients** — every color transition has texture, grain, or noise variation appropriate to the medium
- [ ] **Edges are imperfect** — edges behave as the medium dictates: paint bleeds, paper tears, ink spreads, charcoal scatters
- [ ] **Color mixing matches the medium** — pigment: subtractive mix; ink overprint: multiply; collage: no mixing (opaque overlap); drawing: additive darkening
- [ ] **Marks show process** — the viewer should be able to imagine *how* each mark was made (brush stroke, torn paper, carved line, pressed ink, etc.)
- [ ] **Imperfections exist** — every medium has its own accidents. Identify what imperfections YOUR medium produces and include them
- [ ] **No uniform noise** — real texture has structure specific to the medium. Canvas weave ≠ paper grain ≠ halftone dots ≠ wood grain

### Technical integrity

- [ ] **No smoothstep zone gates** — search for `smoothstep` or `sstep` applied to position coordinates as technique gates
- [ ] **No "only in the lower/upper X%"** — position-based technique confinement is zone-gating in disguise
- [ ] **Every technique has material interaction** — every layer reads the current surface before modifying it
- [ ] **Discrete marks at low alpha** — visible marks (strokes, dots) should be alpha 12-40, not 50+
- [ ] **Atmospheric + textural passes** — any technique that should be visible at both distance and close-up needs two passes
- [ ] **Noise frequencies scale with S** — divide frequencies by S so patterns maintain size at higher resolution
- [ ] **Absolute sizes scale with S** — stroke weights, blur radii, mark sizes multiply by S
- [ ] **No technique parameters copied blindly from notebooks** — every parameter was verified against the actual surface state in the composition
- [ ] **Techniques match the artwork's medium** — don't default to oil-painting techniques (glazing, scumbling, soak-stain) for every artwork. A collage needs cut paper. A watercolor needs wet-on-wet bleeding. A print needs ink layers and registration. Match the implementation to the spec's medium.
- [ ] **Real source material used where appropriate** — if the spec calls for found imagery, text, textures, or photographic elements, real images were sourced and composited, not simulated with procedural noise
- [ ] **No code/architecture reuse from previous projects** — layer function names, blend mode choices, spatial strategies, and color palettes should be derived from THIS spec, not copied from previous work
- [ ] **Color palette is unique to this artwork** — derived from the spec's described colors, the reference artworks studied in Phase 1, and the medium's color behavior. Not the same warm-to-cool gradient every time.
