# Perlin & Simplex Noise

## What it looks like
Organic, cloud-like patterns with smooth transitions. You see rolling hills, flowing curves, or gentle gradients that feel natural rather than random. The noise creates soft variation without harsh edges.

## How it works  
Perlin and Simplex noise generate pseudo-random gradients at grid points and interpolate smoothly between them. Unlike random(), neighboring values are correlated, creating coherent patterns. Simplex noise is a faster variant with less directional artifacts. Artists sample noise at different coordinates to get smooth, organic variation.

## Parameters
- **octaves**: layers of noise at different scales
- **frequency**: how zoomed in/out the pattern is
- **amplitude**: how intense the variation is

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  loadPixels();
  for (let x = 0; x < width; x++) {
    for (let y = 0; y < height; y++) {
      let n = noise(x * 0.01, y * 0.01);
      let bright = n * 255;
      let idx = (x + y * width) * 4;
      pixels[idx] = bright;
      pixels[idx + 1] = bright;
      pixels[idx + 2] = bright;
      pixels[idx + 3] = 255;
    }
  }
  updatePixels();
}
```

## Combinations

**Typical role:** foundation — the base randomness primitive for organic spatial variation

**Works beautifully with:**
- **domain-warping**: Noise distorts other noise for turbulent, complex patterns
- **flow-fields**: Noise creates directional forces — angle = noise(x,y) * TAU
- **fbm-noise**: Layered Perlin octaves for multi-scale detail — FBM is built on Perlin
- **noise-density-scatter**: Noise as probability field for organic element placement

**Creates tension with:**
- grid-layout: Noise is continuous; grids are discrete. Use noise to modulate grid properties (cell color, size) rather than fighting the structure.

**Medium fit:** fine-pencil, watercolor-wash

**Explore from here:**
- If you like organic variation → also look at fbm-noise for richer multi-scale texture
- If you want sharper features → try ridged noise (abs of noise) or worley/cellular noise
- To invent something new → try 3D noise sliced at different Z values over time for evolving patterns

## Art Blocks examples
- 720 Minutes by Alexis André
- Apparitions by Aaron Penne
- Bubble Blobby by Jason Ting
- Ceramics by Charlotte Dann
- Cerebellum by Laya Mathikshara & Santiago
