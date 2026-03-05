# Gradient Systems

## What it looks like
Smooth color transitions from one hue to another. You see gradual shifts—light to dark, warm to cool, or across a spectrum. Gradients add depth and atmosphere.

## How it works  
Gradients interpolate between colors. Linear gradients map position to color stops. Radial gradients spread from a center. Artists use lerp or color space math (HSB, LAB) to calculate intermediate colors.

## Parameters
- **start & end colors**: gradient endpoints
- **direction**: linear angle or radial center
- **color space**: RGB, HSB, or LAB

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  let c1 = color(255, 100, 150);
  let c2 = color(50, 150, 255);
  
  for (let y = 0; y < height; y++) {
    let inter = map(y, 0, height, 0, 1);
    stroke(lerpColor(c1, c2, inter));
    line(0, y, width, y);
  }
}
```

## Combinations

**Typical role:** color / tone — creates smooth tonal transitions and color fields

**Works beautifully with:**
- **particle-systems**: Particles colored by gradient position — location determines hue
- **signed-distance-fields**: Gradients map to SDF distances — color radiates from shape boundaries
- **domain-warping**: Warp gradient coordinates for organic, non-linear color transitions
- **layered-composition**: Different gradients per layer create atmospheric depth

**Creates tension with:**
- posterize-quantization: Gradients want smoothness; posterize wants bands. The tension creates topographic color maps.
- stroke-hatching: Hatching builds tone through line density, gradients through color blending. They can coexist if hatching modulates gradient.

**Medium fit:** watercolor-wash, ceramic-glaze, oil-impasto

**Explore from here:**
- If you like smooth color → also look at cosine-gradient-palette for procedural palettes
- If you want more texture → combine with noise-density-scatter to break up gradient uniformity
- To invent something new → try gradients whose direction follows flow-fields instead of being linear/radial

## Art Blocks examples
- Bubble Blobby by Jason Ting
- Pigments by Darien Brito
- Cryptoblots by Daïm Aggott-Hönsch
- Elementals by Michael Connolly
- Endless Nameless by Rafaël Rozendaal
