# Stochastic Brush Rendering


## Preview
![stochastic-brush-rendering preview](../previews/stochastic-brush-rendering.png)

## What it looks like
Soft, grainy marks that look like pencil or charcoal dragged across textured paper. Instead of solid lines, each stroke is a cloud of scattered particles that cluster along the stroke path, denser at the center and sparser at the edges. The result has that dusty, fibrous quality of dry media — graphite, charcoal, pastel — where pigment particles land individually on the paper surface.

## How it works
For each point along a stroke path, scatter N particles randomly within a radius that varies with pressure. Each particle's position is offset from the center using a probability distribution (Gaussian for pencil, uniform for charcoal). Opacity of each particle is modulated by distance from center and a random factor. The scatter radius, particle count, and falloff curve together control whether the mark reads as a hard pencil, soft charcoal, or chalky pastel.

## Parameters
- **scatter radius**: how far particles spread from the stroke center (2-30 px)
- **particle density**: number of dots per stroke step (5-80)
- **falloff curve**: Gaussian sigma or power exponent controlling edge softness (0.3-3.0)
- **opacity range**: min/max alpha for individual particles (0.02-0.15)
- **grain response**: how much underlying paper texture modulates particle placement (0-1)

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(245, 242, 235);
  noLoop(); randomSeed(42); noiseSeed(42);

  // Draw several stochastic brush strokes
  for (let s = 0; s < 12; s++) {
    let x = random(50, 350), y = random(50, 350);
    let col = color(40 + random(30), 30 + random(20), 25 + random(15));
    let radius = random(5, 20);

    for (let i = 0; i < 200; i++) {
      let t = i / 200;
      let cx = x + noise(s, t * 3) * 200 - 100;
      let cy = y + noise(s + 50, t * 3) * 150 - 75;
      // Scatter particles around center
      for (let p = 0; p < 15; p++) {
        let angle = random(TWO_PI);
        let dist = randomGaussian(0, radius * 0.4);
        let px = cx + cos(angle) * abs(dist);
        let py = cy + sin(angle) * abs(dist);
        let a = map(abs(dist), 0, radius, 40, 5);
        noStroke(); fill(red(col), green(col), blue(col), a);
        ellipse(px, py, random(0.5, 2.5));
      }
    }
  }
}
```

## Combinations

**Typical role:** mark / texture — creates the individual mark quality of dry drawing media

**Works beautifully with:**
- **flow-fields**: Scatter particles along flow lines for directional charcoal strokes
- **stroke-hatching**: Stochastic rendering applied to hatching strokes gives pencil-quality cross-hatching
- **texture-synthesis**: Paper grain modulates where particles land — lighter touch on peaks, denser in valleys
- **erode-dilate**: Slight dilation after scattering simulates charcoal dust spreading into paper

**Creates tension with:**
- **blend-modes**: Stochastic marks are already semi-transparent; additive blend can over-brighten. Use multiply or darken modes.

**Medium fit:** fine-pencil, charcoal-conte, ink-on-paper

**Explore from here:**
- If you like the grainy quality → also look at alpha-spatter, noise-density-scatter
- If you want more control → combine with pressure-simulation for variable-width strokes
- To invent something new → try stochastic rendering where particle count responds to audio input

## Art Blocks examples
- Fidenza by Tyler Hobbs (subtle stroke texture)
- Memories of Qilin by Emily Xie
- Meridian by Matt DesLauriers
