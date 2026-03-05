# Alpha Spatter

## What it looks like
Spray-paint-like spatter where pigment covers some areas densely and leaves irregular holes and voids. The texture feels like ink misted through a screen or paint thrown from a loaded brush, with organic gaps where the spray missed.

## How it works
For each pixel or particle, sample a noise field. If the noise value falls below a threshold, the point is fully transparent (creating holes). Values above the threshold get their alpha boosted by a power curve, concentrating opacity in the high-noise areas. The result is organic clusters of dense pigment with natural-looking voids. Varying the threshold and power exponent controls sparsity.

## Parameters
- **threshold**: noise cutoff below which alpha is zero (0.3-0.6)
- **power curve**: exponent applied to surviving values (1.5-4.0)
- **noise scale**: size of the spatter clusters
- **base color**: the pigment color before alpha modulation

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(245);
  loadPixels();
  let threshold = 0.42;
  let power = 2.5;

  for (let x = 0; x < width; x++) {
    for (let y = 0; y < height; y++) {
      let n = noise(x * 0.015, y * 0.015);
      let a = 0;
      if (n > threshold) {
        a = pow((n - threshold) / (1.0 - threshold), power) * 255;
      }
      let idx = (y * width + x) * 4;
      pixels[idx] = 25;
      pixels[idx + 1] = 20;
      pixels[idx + 2] = 60;
      pixels[idx + 3] = a;
    }
  }
  updatePixels();
}
```

## Combinations

**Typical role:** detail / texture — adds organic spray and granulation over existing forms

**Works beautifully with:**
- **particle-systems**: Scatter particles then apply spatter alpha to each — particles become spray dots
- **blend-modes**: Layer multiple spatter passes with multiply or screen for deep pigment effects
- **texture-synthesis**: Spatter as a texture mask over other elements — reveals surface underneath
- **flow-fields**: Spatter density follows flow direction, like spray paint aimed along a wind
- **posterize-quantization**: Stencil-cut hard edges + soft spray around them = classic street art

**Creates tension with:**
- gradient-systems: Both create tonal variation — spatter adds noise where gradients want smoothness. Keep one dominant.

**Medium fit:** spray-paint, watercolor-wash, ink-on-paper, charcoal-conte

**Explore from here:**
- If you like the scattered texture → also look at noise-density-scatter, texture-synthesis
- If you want denser coverage → combine with layered-composition for multiple spray passes
- To invent something new → try spatter that follows a signed-distance-field boundary

## Art Blocks examples
- INK by Iskra Velitchkova
- Avventura by Aaron Penne
- Fragments of an Infinite Field by Monica Rizzolli
