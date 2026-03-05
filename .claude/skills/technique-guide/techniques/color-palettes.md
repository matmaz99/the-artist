# Color Palette Systems

## What it looks like
A curated selection of harmonious colors applied consistently across an artwork. You see coordinated hues that feel intentional—whether muted pastels, vibrant complements, or monochromatic shades. The palette unifies the piece and sets its emotional tone.

## How it works  
The artist defines arrays of RGB or HSB values representing different color schemes. During generation, the hash or parameters select one palette, and shapes draw from its colors either sequentially, randomly, or based on rules. Some systems weight colors differently, making certain hues more prominent. Advanced implementations use color theory to ensure harmony.

## Parameters
- **palette**: which color scheme to use
- **color selection method**: random, sequential, or rule-based
- **weighting**: probability distribution across colors

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  let palettes = [
    ['#264653', '#2a9d8f', '#e9c46a', '#f4a261', '#e76f51'],
    ['#001219', '#005f73', '#0a9396', '#94d2bd', '#e9d8a6'],
    ['#03071e', '#370617', '#6a040f', '#9d0208', '#d00000']
  ];
  
  let palette = random(palettes);
  background(255);
  
  for (let i = 0; i < 20; i++) {
    fill(random(palette));
    let x = random(50, 350);
    let y = random(50, 350);
    let size = random(30, 80);
    ellipse(x, y, size);
  }
}
```

## Combinations

**Typical role:** color / foundation — provides the curated color set for the entire artwork

**Works beautifully with:**
- **flow-fields**: Palettes guide particle colors along paths — map flow distance to palette position
- **layered-composition**: Each layer uses different palette colors for clear depth separation
- **cosine-gradient-palette**: Cosine palettes as an algorithmic alternative to hand-picked swatches
- **weighted-random**: Weighted palette sampling — dominant color appears 60%, accents 10% each

**Creates tension with:**
- hsb-hsl-color: Both define color strategy — pick one approach. Palettes for curated harmony, HSB for computed variation.

**Medium fit:** gouache-layers, watercolor-wash, oil-impasto, ceramic-glaze

**Explore from here:**
- If you like curated color → also look at cosine-gradient-palette for infinite smooth variation
- If you want mood shifts → animate palette selection over time with temporal-animation
- To invent something new → try palettes extracted from photographs via posterize-quantization

## Art Blocks examples
- Fidenza by Tyler Hobbs
- Anticyclone by William Mapan
- Archetype by Kjetil Golid
- Apparitions by Aaron Penne
- Asemica by Emily Edelman, Dima Ofman, Andrew Badr
