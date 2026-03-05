# Noise Density Scatter

## What it looks like
Elements clustered in organic groups with natural-looking empty spaces between them. Dense colonies of dots, marks, or shapes appear where the noise is favorable, while voids open up where it is not. The distribution feels biological, like lichen growth or forest clearings.

## How it works
Generate candidate positions (grid or random). For each position, sample a noise field. Only place an element if the noise value is below a threshold. Areas where noise is consistently low become dense clusters; areas where noise is high remain empty. Adjusting the threshold controls overall density, while noise scale controls the size of clusters and voids.

## Parameters
- **threshold**: noise cutoff for placement (0.3-0.6)
- **noise scale**: size of clusters/voids
- **element density**: candidate points per area
- **element type**: what gets placed (dot, shape, glyph)

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(245);
  noStroke();
  fill(30, 60, 80);

  let threshold = 0.45;
  let spacing = 6;

  for (let x = spacing; x < width; x += spacing) {
    for (let y = spacing; y < height; y += spacing) {
      let n = noise(x * 0.01, y * 0.01);
      if (n < threshold) {
        let sz = map(n, 0, threshold, 4, 1);
        ellipse(x + random(-1, 1), y + random(-1, 1), sz);
      }
    }
  }
}
```

## Combinations

**Typical role:** distribution — places elements in organic clusters using noise as probability

**Works beautifully with:**
- **perlin-simplex-noise**: The density field that controls placement — noise is the probability map
- **particle-systems**: Scatter particles using noise acceptance/rejection for organic clumping
- **weighted-random**: Combine noise density with weighted size/color selection for rich variety
- **circle-packing**: Noise-modulated packing density — dense clusters and sparse voids

**Creates tension with:**
- grid-layout: Grid wants uniform spacing; noise scatter wants organic clustering. Use noise to modulate grid cell occupancy as a compromise.

**Medium fit:** spray-paint, charcoal-conte

**Explore from here:**
- If you like organic distribution → also look at circle-packing, voronoi-tessellation
- If you want more control → combine with spatial-partitioning for efficient large-scale scatter
- To invent something new → try scatter where density is driven by audio-reactive input

## Art Blocks examples
- Fragments of an Infinite Field by Monica Rizzolli
- Subscapes by Matt DesLauriers
- Garden, Pair by Matto
