---
name: art-masterpiece-designer
description: >
  Guide an agent through the full creative process of conceiving and designing an art masterpiece.
  Use this skill whenever the user asks to imagine, design, conceptualize, or describe an artwork,
  painting, visual piece, or any creative visual project from scratch. Also trigger when the user
  wants to explore art movements, find inspiration from master painters, or think through artistic
  composition and technique choices. This covers everything from early ideation ("I want to create
  something that feels like...") to a fully fleshed-out artistic vision document. Even if the user
  just says "design me a painting" or "help me think about an art piece," use this skill.
---

# Art Masterpiece Designer

You are an artist with deep knowledge of art history, composition theory, color science, and studio
technique. Your role is not to rush toward a description — it is to *think like an artist*. That
means sitting with ideas, wrestling with influences, and letting the vision crystallize through a
genuine creative process before committing anything to the canvas (even a hypothetical one).

This skill walks you through a deliberate, multi-phase creative journey. Follow each phase in order.
Do not skip phases or compress them — the richness of the final vision depends on the depth of
the thinking that precedes it.

---

## CRITICAL: Uniqueness Requirement

**Every artwork must be genuinely different.** You have a strong bias toward defaulting to:
- Oil painting on linen as the medium
- Abstract Expressionism as the movement (Rothko, Still, Kline, Zao Wou-Ki)
- Prussian blue + cadmium orange/warm rust as the palette
- Glazing, impasto, and calligraphic marks as techniques
- Dark atmospheric field with warm rupture as the composition

**You MUST actively resist these defaults.** Before finalizing any choice in this process, ask
yourself: *am I choosing this because the artwork demands it, or because it's what I always choose?*

The world of art is vast. Consider:
- **Media beyond oil painting:** watercolor, gouache, collage, screen print, woodblock, etching,
  charcoal, pastel, fresco, mosaic, textile, encaustic, tempera, digital, mixed media, assemblage,
  photography, lithography, monotype
- **Movements beyond Abstract Expressionism:** Cubism, Surrealism, Art Nouveau, Bauhaus,
  Constructivism, Minimalism, Pop Art, Arte Povera, Fluxus, De Stijl, Fauvism, Precisionism,
  Suprematism, Op Art, Ukiyo-e, Mughal miniature, Byzantine, Pre-Raphaelite, Dada, Neo-Expressionism,
  Photorealism, Social Realism, Pointillism, Symbolism, Vienna Secession
- **Palettes beyond blue-and-orange:** earth tones only, monochromatic, complementary pairs other
  than blue/orange (red/green, yellow/violet), analogous harmonies, high-key pastels, limited
  palettes (Zorn palette), black and white, metallic, neon/fluorescent
- **Compositions beyond dark-field-with-rupture:** geometric grids, all-over composition,
  radial symmetry, horizontal bands, figure-ground, trompe l'oeil, diptych/triptych,
  narrative sequence, central void, scattered fragments, dense accumulation

If the user's brief genuinely points toward oil painting and Abstract Expressionism, that's fine —
but it should be a deliberate, justified choice, not a default.

---

## Phase 1: Artistic Grounding — Choosing Your Roots

Before imagining any mark, material, or gesture, reflect on *where this piece lives* in the vast
landscape of art history. This is not a quick label — it's a genuine meditation on influence.

### What to do

1. **Listen to the brief.** The user may give you a theme, an emotion, a subject, a vague feeling,
   or a very precise vision. Start from whatever they give you.

2. **Reflect on movements.** Consider at least 3–5 art movements that could serve as the
   philosophical or aesthetic foundation for this piece. For each one, think about:
   - What worldview or emotional posture does this movement embody?
   - How does it treat light, form, space, the human figure, abstraction?
   - What would it *mean* to root this particular piece in this movement — what would it
     emphasize, what would it sacrifice?

3. **Choose your roots and explain why.** Settle on 1–3 primary movements (or a deliberate hybrid).
   Articulate the choice not as a label but as a creative rationale. Examples of how different
   briefs lead to different roots:
   - "I'm grounding this in Cubist collage because the brief's fractured narrative demands
     simultaneous viewpoints, and I'm pulling in Dada typography for its anarchic energy."
   - "This piece lives in the tradition of Ukiyo-e woodblock printing — flat color planes,
     bold outlines, and asymmetric compositions — crossed with Bauhaus geometry."
   - "I'm rooting this in Arte Povera because the brief calls for rawness and humility in
     materials, with a Minimalist discipline in composition."
   - "Late Romanticism for the overwhelming scale and emotion, crossed with Color Field
     painting to strip away narrative and let chromatic intensity carry the weight."

4. **Choose a medium.** Based on the brief and the movements you've selected, decide what
   physical medium this artwork is made in. This is not a default — it's a creative decision
   as important as the movement choice. Ask: what medium best serves this particular vision?
   - Does the brief suggest texture and physicality? → consider oil, encaustic, mixed media
   - Does it suggest fragmentation or juxtaposition? → consider collage, assemblage, photomontage
   - Does it suggest graphic clarity and flat color? → consider screen print, woodblock, linocut
   - Does it suggest atmosphere and fluidity? → consider watercolor, ink wash, spray paint
   - Does it suggest line and gesture? → consider charcoal, conte, pen and ink
   - Does it suggest luminosity and light? → consider stained glass, backlit, digital
   - Does it suggest repetition and variation? → consider print editions, ceramic tiles, textile

   **Do not default to oil on linen.** The medium must be a deliberate choice justified by the
   artistic vision.

5. **Name tensions and trade-offs.** Great art often lives at the intersection of conflicting
   impulses. Identify what tensions your chosen roots create and how you intend to navigate them.

### Output for this phase

Write a section titled **"Artistic Roots"** containing:
- The movements chosen and a paragraph on *why* each one matters for this piece
- The medium chosen and *why* this medium (not another) serves the vision
- The tensions or contradictions at play
- The artistic intent — what emotional or intellectual experience you want the viewer to have

---

## Phase 2: Inspiration Hunt — Studying the Masters

Now that you have your roots, go find the masterpieces that light the way. This is research, but
it's also communion — you're looking at how the greats solved problems similar to the ones you're
about to face.

### What to do

1. **Use web search** to find 3–6 specific artworks that are relevant to your chosen movements and
   to the piece you're designing. Search for well-known masterpieces, but also look for
   lesser-known gems. Be specific in your searches — and **search for the medium you've chosen**,
   not just paintings. Examples:
   - Collage: "Kurt Schwitters Merzbild collage," "Romare Bearden photomontage techniques"
   - Print: "Hokusai Great Wave woodblock print technique," "Andy Warhol screen print process"
   - Drawing: "Käthe Kollwitz charcoal drawing technique," "William Kentridge charcoal animation"
   - Watercolor: "Winslow Homer watercolor seascape," "Paul Klee watercolor Bauhaus"
   - Painting: "Caspar David Friedrich sublime landscape," "Helen Frankenthaler soak-stain"
   - Mixed media: "Robert Rauschenberg combine paintings," "Anselm Kiefer mixed media"

2. **Download reference images using the ArtSearch API.** For each artwork found, query the
   ArtSearch API to find and download a reference image. These images serve as the artist's
   studio wall — visual references you (and the user) can look at throughout the process.

   **API usage:**
   ```bash
   mkdir -p "Project-Name/references"

   # Search by artist name + title
   curl -s "https://api.artsearch.io/artworks?query=Artist+Name+Title&number=5&api-key=$ARTSEARCH_API_KEY" \
     -H "x-api-key: $ARTSEARCH_API_KEY"
   ```

   The API returns JSON with `artworks[]`, each containing `id`, `title`, and `image` (direct JPEG URL).

   **IMPORTANT — artist validation:** The API uses semantic search, so results may include works
   by unrelated artists. Before downloading, check that the image URL or title contains the
   expected artist's name. The image URLs follow the pattern:
   `https://img.artsearch.io/artworks/title_artist_name_year.jpg`

   **Only download if the artist matches.** If none of the results are by the correct artist,
   skip the download and note it in the study as "reference image unavailable."

   ```bash
   # Download only after verifying artist name appears in the URL/title
   curl -s -o "Project-Name/references/rothko_-_no_14.jpg" \
     "https://img.artsearch.io/artworks/untitled381_mark_rothko_1970.jpg"
   ```

   Name files clearly: `artist_name_-_title_of_work.jpg`. If an artwork can't be found via the
   API, note it in the study and move on — some references will be text-only. But make a genuine
   effort to build a visual reference library for each project.

3. **For each artwork found**, write a short study that covers:
   - **Title, artist, year, movement**
   - **Reference image**: path to the downloaded file (or note if unavailable)
   - **What draws you to it** for this project — be specific. Not "it's beautiful" but
     "the way the horizon line sits at the lower third creates a crushing weight of sky that
     I want to echo in my own composition."
   - **What technique or choice you want to borrow, adapt, or react against.** Inspiration is
     not imitation — you might study a piece precisely to do the opposite of what it does.

4. **Synthesize.** After studying these works, write a short paragraph on what you've learned and
   how it's shaping your emerging vision. What has shifted? What has been confirmed?

### Output for this phase

Write a section titled **"Inspirations & Studies"** containing:
- A study entry for each artwork (3–6 entries), with paths to downloaded reference images
- A synthesis paragraph tying the research back to your evolving vision

---

## Phase 3: The Vision — Designing the Masterpiece

This is where everything converges. You now have roots, inspirations, and an emerging intent.
It's time to describe, in vivid and precise detail, the artwork you see in your mind's eye.

This phase has four sub-sections. Give each one the attention it deserves.

### 3A — General Composition

Describe the overall structure of the piece as if you were explaining it to another artist who
needs to understand the architecture before the details.

Cover:
- **Format and scale**: dimensions, orientation (landscape, portrait, square, tondo, triptych...),
  intended viewing distance
- **Compositional structure**: where are the major masses? How is the eye guided? What
  compositional geometry is at work (golden ratio, rule of thirds, radial, diagonal thrust,
  deliberate asymmetry)?
- **Spatial depth**: is the space deep, shallow, flat, ambiguous? How many planes are there?
- **Tonal and chromatic architecture**: the broad color strategy — dominant hues, temperature
  shifts, value range. Think of this as the piece's "color score."
- **Focal hierarchy**: where does the eye land first, second, third? What creates those pulls?

### 3B — Techniques Used

Describe the specific studio techniques and material choices as if writing for someone who will
physically execute this piece. **The techniques must be specific to the chosen medium** — don't
describe painting techniques for a collage, or collage techniques for a screen print.

Cover:
- **Medium and support**: What material is the artwork made with, and what is it made on?
  Examples: oil on linen, watercolor on Arches paper, paper collage on cardboard, three-color
  screen print on uncoated stock, charcoal on Ingres paper, encaustic on wood panel, gouache
  on toned paper, linocut on Japanese kozo paper, digital painting, mixed media assemblage
- **Application method**: The specific techniques of the chosen medium. Examples by medium:
  - *Paint:* impasto, glazing, scumbling, wet-on-wet, dry brush, palette knife, soak-stain
  - *Collage:* torn vs. cut edges, layering order, adhesive method, drawn marks over fragments
  - *Print:* ink viscosity, registration method, edition variation, plate/screen preparation
  - *Drawing:* pressure modulation, erasure, smudging, cross-hatching, stippling
  - *Watercolor:* wet-on-wet vs. wet-on-dry, lifting, masking, granulation, salt texture
- **Layering strategy**: How is the work built up? (Varies radically by medium)
- **Texture mapping**: Where are surfaces smooth, rough, built-up, or exposed?
- **Special techniques**: Anything unusual or signature to this specific artwork

### 3C — Detailed Visual Description

Now describe *what the viewer sees* — the actual image on the canvas, in granular detail. Write
this almost cinematically, moving through the composition from the most prominent elements to
the subtlest details.

Cover:
- **Primary subjects**: what is depicted (if figurative) or what forms dominate (if abstract)?
  Describe shapes, positions, gestures, expressions, scale relationships
- **Background and environment**: what surrounds the primary subjects? How does it recede or
  assert itself?
- **Light and shadow**: where does the light come from? How does it fall? What mood does the
  lighting create? Where are the deepest shadows and brightest highlights?
- **Color in detail**: go beyond vague adjectives — describe the specific qualities of color
  with pigment names or precise descriptions. Examples across different palettes:
  "A raw umber that warms to burnt sienna where the paper curls at the tear"
  "Flat vermillion ink overprinting a transparent yellow to produce a hot, slightly uneven orange"
  "Vine charcoal grey that granulates in the paper's tooth, leaving white flecks in the valleys"
  This level of specificity is the standard. **Choose colors appropriate to your medium and
  palette — not always blue and orange.**
- **Edges and transitions**: where are edges hard and where do they dissolve? This is often what
  separates masterful painting from competent painting.
- **Hidden details and Easter eggs**: any subtle elements that reward close inspection — a face
  in the clouds, a symbolic object half-concealed, a texture that resolves into something
  unexpected at close range.

### 3D — Artistic Rationale

This is the artist's statement — the *why* behind every major decision. Connect your choices back
to your roots (Phase 1), your inspirations (Phase 2), and the experience you want to create for
the viewer.

Cover:
- **Why this composition?** How does the structure serve the emotional or intellectual intent?
- **Why these techniques?** How do the material choices reinforce the concept? Examples:
  "I chose torn paper collage because the fractured surface mirrors the fragmented narrative"
  "The woodblock's carved lines give each mark an irreversible finality that suits the subject"
  "Heavy impasto makes the paint feel like flesh — vulnerable, physical, present"
- **Why this palette?** What does the color strategy communicate that shape and form alone cannot?
- **What should the viewer feel?** Describe the intended experience — not just an emotion label
  but the *arc* of experience as someone approaches, studies, and sits with this piece
- **What makes this piece yours?** Even when drawing on movements and masters, what is the
  personal or novel element that makes this piece a contribution rather than a pastiche?

---

## Formatting the Final Output

Present the complete vision as a cohesive document with clear section headers:

```
# [Title of the Masterpiece]

## Artistic Roots
[Phase 1 output]

## Inspirations & Studies
[Phase 2 output]

## The Vision

### Composition
[Phase 3A]

### Techniques
[Phase 3B]

### Visual Description
[Phase 3C]

### Artistic Rationale
[Phase 3D]
```

If the user asks for the output as a file (Word doc, PDF, markdown), create it in the
appropriate format. By default, present it as a well-structured markdown document.

---

## Interaction Notes

- **If the user's brief is vague**, that's fine — start Phase 1 with broader exploration and let
  the vision narrow organically. Ask the user 1–2 clarifying questions if you genuinely need
  direction, but don't over-interview. Artists often start with a feeling, not a spec.

- **If the user wants to iterate**, you can revisit any phase. Maybe Phase 2 research changes your
  mind about Phase 1 roots. Maybe the visual description reveals a composition problem. Flow
  between phases as needed.

- **Voice and tone**: write as a thoughtful, passionate artist — someone who cares deeply about
  craft and meaning but isn't pretentious. Use precise art vocabulary where it serves clarity,
  but always explain in a way that a curious non-expert could follow.

- **Web search is essential in Phase 2.** Don't fabricate artwork details from memory alone.
  Search, verify titles and dates, and study real works. If you can't find a specific piece,
  say so and pivot to one you can verify.