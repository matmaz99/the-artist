# Ghost Stroke Doubling

## What it looks like
Every line appears with a faint, slightly offset echo behind it, like a spectral afterimage or a shadow cast by the stroke. The doubled marks create a sense of depth, vibration, or imprecise printing registration.

## How it works
Each stroke is drawn twice. First, a faint copy is rendered at low opacity with a small spatial offset (typically a few pixels in a consistent direction). Then the primary stroke is drawn at full opacity on top. The offset direction can be fixed (like a drop shadow) or vary per stroke. The ghost opacity is usually 10-25% of the primary.

## Parameters
- **offset x/y**: displacement of the ghost stroke
- **ghost opacity**: transparency of the echo (0.05-0.3)
- **ghost color**: same as primary or shifted (often warmer/cooler)
- **blur**: whether the ghost is drawn with thicker weight for softness

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(245);

  let ox = 4, oy = 3;

  for (let i = 0; i < 30; i++) {
    let x1 = random(40, 360), y1 = random(40, 360);
    let x2 = x1 + random(-80, 80), y2 = y1 + random(-80, 80);

    // ghost stroke
    stroke(80, 60, 120, 30);
    strokeWeight(2.5);
    line(x1 + ox, y1 + oy, x2 + ox, y2 + oy);

    // primary stroke
    stroke(20, 15, 40, 200);
    strokeWeight(1.8);
    line(x1, y1, x2, y2);
  }
}
```

## Combinations

**Typical role:** detail / atmosphere — adds spectral echoes behind marks for depth and imprecision

**Works beautifully with:**
- **line-drawing**: Any line-based work benefits from ghost doubling — adds hand-drawn imprecision
- **flow-fields**: Ghost echoes on flow traces add atmospheric depth like smoke trails
- **blend-modes**: Multiply or screen blending between ghost and primary controls the echo character
- **fat-line-stroke**: Ghost behind thick strokes creates a shadow/depth effect like paint showing through paper

**Creates tension with:**
- posterize-quantization: Ghosts are subtle transparency; posterize eliminates subtlety. Use ghosts at full strength if combining.
- blur-post-processing: Blur already softens marks — adding ghost doubling on top can feel redundant. Pick one softening strategy.

**Medium fit:** fine-pencil, charcoal-conte, etching-printmaking, watercolor-wash

**Explore from here:**
- If you like the echo effect → also look at motion-trails for longer persistence
- If you want more atmosphere → combine with layered-composition for ghosts at different depths
- To invent something new → try ghosts that drift in a different direction than the primary mark (wind-blown ink)

## Art Blocks examples
- Apparitions by Aaron Penne
- Meridian by Matt DesLauriers
- Bauhaus Blocks by Piter Pasma
