# Hash-Based Randomness

## What it looks like
Deterministic variety—every output looks different but regenerates identically from the same input. The hash creates unique parameter choices that define the piece.

## How it works  
A hash (like a transaction ID) seeds a pseudo-random number generator. The PRNG produces a predictable sequence. Artists extract values to control colors, shapes, positions. Same hash = same artwork every time.

## Parameters
- **hash**: the seed value
- **extraction method**: which bytes for which parameters
- **mapping**: converting hash to usable ranges

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
  
  let hashValue = 'ab3f9821cd';
  let seed = parseInt(hashValue.substring(0, 8), 16);
  randomSeed(seed);
}

function draw() {
  background(255);
  let numShapes = int(random(5, 15));
  
  for (let i = 0; i < numShapes; i++) {
    fill(random(255), random(255), random(255), 150);
    ellipse(random(width), random(height), random(20, 100));
  }
}
```

## Combinations

**Typical role:** utility / seed — provides deterministic randomness from input values

**Works beautifully with:**
- **color-palettes**: Hash selects palette and color indices — deterministic but varied
- **metadata-driven**: Hash determines features from token properties
- **prng-systems**: Hash seeds the PRNG for reproducible sequences
- **weighted-random**: Hash output feeds weighted selection for controlled variety

**Creates tension with:**
- perlin-simplex-noise: Both provide randomness but at different scales — hash is per-element, noise is spatial. They complement more than conflict.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like deterministic variety → also look at prng-systems, weighted-random
- If you want spatial variation → combine hash with grid-layout — each cell gets unique hash
- To invent something new → try using hash to select which technique draws in each region

## Art Blocks examples
- Aerial View by daLenz
- Apparitions by Aaron Penne
- Calian by Eric De Giuli
- Construction Token by Jeff Davis
- Dynamic Slices by pxlq
