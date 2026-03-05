# Erode / Dilate

## What it looks like
Marks that appear to bleed into the surface like ink soaking into wet paper, or conversely, marks that have been eaten away at their edges. Erosion thins strokes and opens gaps. Dilation spreads marks outward and fills small holes. The combination simulates natural ink and paper interaction.

## How it works
Morphological operations on a pixel grid. Erosion replaces each pixel with the minimum value in its neighborhood (typically a 3x3 or 5x5 kernel), shrinking bright regions. Dilation replaces each pixel with the maximum, expanding bright regions. Running erosion then dilation (opening) removes small marks and smooths edges. Dilation then erosion (closing) fills gaps and bleeds marks together. The operations work on the alpha or brightness channel.

## Parameters
- **kernel size**: neighborhood radius (1-5 pixels)
- **iterations**: number of passes (more = stronger effect)
- **operation order**: erode-dilate (opening) vs dilate-erode (closing)
- **channel**: which channel to process (alpha, brightness, per-channel)

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(200, 200);
  background(245);
  stroke(30);
  strokeWeight(2);
  for (let i = 0; i < 40; i++) {
    let x = random(width), y = random(height);
    line(x, y, x + random(-30, 30), y + random(-30, 30));
  }

  loadPixels();
  let src = pixels.slice();
  let w = width, h = height;
  let kern = 2;

  // dilate pass: max of neighbors (spreads dark marks on light bg, so use min)
  for (let x = kern; x < w - kern; x++) {
    for (let y = kern; y < h - kern; y++) {
      let minVal = 255;
      for (let dx = -kern; dx <= kern; dx++) {
        for (let dy = -kern; dy <= kern; dy++) {
          let idx = ((y + dy) * w + (x + dx)) * 4;
          minVal = min(minVal, src[idx]);
        }
      }
      let i = (y * w + x) * 4;
      pixels[i] = pixels[i + 1] = pixels[i + 2] = minVal;
    }
  }
  updatePixels();
}
```

## Combinations

**Typical role:** material / post-process — simulates ink bleed, paint spread, or mark weathering

**Works beautifully with:**
- **texture-synthesis**: Morphological ops create natural paper/ink textures — eroded marks look aged
- **line-drawing**: Erode thin lines to fragile traces, dilate for bold ink-soaked marks
- **blend-modes**: Apply erosion/dilation to mask layers before compositing for rich edge effects
- **stroke-hatching**: Dilate hatching lines so they bleed together like ink on wet paper

**Creates tension with:**
- signed-distance-fields: SDFs produce mathematically clean edges that erosion destroys. That destruction can be beautiful — weathered precision.
- posterize-quantization: Both simplify — erode smooths edges while posterize flattens tone. Choose one as primary simplifier.

**Medium fit:** ink-on-paper, etching-printmaking, charcoal-conte, watercolor-wash, ceramic-glaze

**Explore from here:**
- If you like edge effects → also look at deckled-edge for border-specific treatment
- If you want controlled bleed → combine with signed-distance-fields to erode only near boundaries
- To invent something new → try directional erosion that follows flow-fields — ink bleeds with gravity

## Art Blocks examples
- INK by Iskra Velitchkova
- Washed by Thomas Lin Pedersen
- Bubblegum by Licia He
