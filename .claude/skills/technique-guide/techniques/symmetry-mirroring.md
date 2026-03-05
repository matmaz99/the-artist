# Symmetry & Mirroring

## What it looks like
Perfect reflection across axes or radial symmetry. Shapes that mirror horizontally, vertically, or radiate from a center like a kaleidoscope.

## How it works  
Draw once, then apply transformations (scale(-1, 1) for horizontal flip). Radial symmetry uses rotation: for n-fold symmetry, rotate by 360/n degrees and draw n times.

## Parameters
- **axis**: horizontal, vertical, both, or radial
- **fold count**: number of repetitions
- **offset**: symmetry center point

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  background(255);
  translate(width/2, height/2);
  
  let folds = 8;
  for (let i = 0; i < folds; i++) {
    push();
    rotate(TWO_PI * i / folds);
    drawSection();
    pop();
  }
}

function drawSection() {
  fill(random(255), random(255), random(255), 150);
  noStroke();
  triangle(0, 0, 50, -20, 40, -60);
  ellipse(25, -40, 20);
}
```

## Combinations

**Typical role:** composition — creates reflection or rotational symmetry for balanced, decorative forms

**Works beautifully with:**
- **line-drawing**: Symmetric ornamental patterns — mirrored line work for decorative precision
- **particle-systems**: Mirrored particle trails create kaleidoscopic movement patterns
- **truchet-tiles**: Symmetric tile arrangements for complex repeating patterns
- **substitution-tiling**: Tiling symmetry groups create mathematically rich compositions

**Creates tension with:**
- differential-growth: Natural growth is asymmetric — forced symmetry looks artificial. Bilateral is the maximum natural symmetry.
- flow-fields: Flow is inherently directional; symmetry wants balance. Use symmetric flow fields for natural-looking results.

**Medium fit:** woven-textile

**Explore from here:**
- If you like balanced composition → also look at grid-layout for structural balance
- If you want imperfect symmetry → add noise-density-scatter to break perfect reflection slightly
- To invent something new → try symmetry that gradually breaks down from center to edge using domain-warping

## Art Blocks examples
- Cryptoblots by Daïm Aggott-Hönsch
- Flux by Owen Moore
- HyperHash by Beervangeer
- Quine by Larva Labs
- Synapses by Chaosconstruct
