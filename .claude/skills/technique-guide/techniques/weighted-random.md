# Weighted Random Selection

## What it looks like
Controlled randomness where some outcomes are more common than others. Visual variety with intentional distribution.

## How it works  
Assign weights to options, create cumulative sum, generate random value, find which range it falls into. Higher weights = more likely selection.

## Parameters
- **weights**: relative probabilities
- **options**: choices to select from

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function weightedChoice(options, weights) {
  let total = weights.reduce((sum, w) => sum + w, 0);
  let r = random(total);
  
  for (let i = 0; i < options.length; i++) {
    if (r < weights[i]) return options[i];
    r -= weights[i];
  }
  return options[options.length - 1];
}

function draw() {
  background(255);
  
  let colors = ['red', 'blue', 'green', 'yellow'];
  let weights = [50, 20, 10, 5]; // Red 50%, blue 20%, etc.
  
  for (let i = 0; i < 200; i++) {
    fill(weightedChoice(colors, weights));
    let x = random(width);
    let y = random(height);
    ellipse(x, y, 20);
  }
  
  // Red should be most common
}
```

## Combinations

**Typical role:** utility — controls probability distributions so some outcomes are more likely than others

**Works beautifully with:**
- **metadata-driven**: Weights define rarity tiers — common, uncommon, rare, legendary
- **color-palettes**: Weighted color selection — dominant color 60%, accents 10% each
- **apparatus-grid**: Weighted cell merge probability for varied block sizes
- **particle-systems**: Weighted size, speed, or color distributions for natural variety

**Creates tension with:**
- perlin-simplex-noise: Both provide controlled randomness but differently — weights for discrete choices, noise for continuous fields.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like controlled variety → also look at hash-randomness for position-based variation
- If you want visual impact → weight distributions toward extremes (mostly tiny + few huge) for drama
- To invent something new → try weights that change over time — early artworks favor one style, later favor another

## Art Blocks examples
- AlgoRhythms by Han x Nicolas Daniel
- Archetype by Kjetil Golid
- Elementals by Michael Connolly
- Trossets by Anna Carreras
