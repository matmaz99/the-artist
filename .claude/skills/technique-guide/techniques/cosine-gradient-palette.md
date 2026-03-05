# Cosine Gradient Palette

## What it looks like
Smooth, richly varied color gradients that cycle through hues without harsh jumps. Colors flow naturally from warm to cool and back, with the ability to generate an infinite variety of harmonious palettes from just four parameter vectors.

## How it works
Inigo Quilez's cosine palette formula: `color(t) = a + b * cos(2*PI*(c*t + d))`. The four vec3 parameters (a, b, c, d) control the color output for any input t in [0,1]. `a` is the offset (average brightness), `b` is the amplitude (contrast), `c` is the frequency (how many color cycles), and `d` is the phase (hue shift). Each RGB channel gets its own cosine wave, creating smooth color ramps.

## Parameters
- **a (offset)**: vec3 base color, controls overall brightness
- **b (amplitude)**: vec3 color range, controls contrast
- **c (frequency)**: vec3 cycle count per channel
- **d (phase)**: vec3 hue offset per channel

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noStroke();

  // palette params: a, b, c, d (each [r, g, b])
  let a = [0.5, 0.5, 0.5];
  let b = [0.5, 0.5, 0.5];
  let c = [1.0, 1.0, 1.0];
  let d = [0.0, 0.33, 0.67];

  for (let x = 0; x < width; x++) {
    for (let y = 0; y < height; y++) {
      let t = noise(x * 0.005, y * 0.005);
      let r = a[0] + b[0] * cos(TWO_PI * (c[0] * t + d[0]));
      let g = a[1] + b[1] * cos(TWO_PI * (c[1] * t + d[1]));
      let bl = a[2] + b[2] * cos(TWO_PI * (c[2] * t + d[2]));
      fill(r * 255, g * 255, bl * 255);
      rect(x, y, 1, 1);
    }
  }
}
```

## Combinations

**Typical role:** color / algorithm — generates smooth, rich color gradients procedurally

**Works beautifully with:**
- **gradient-systems**: Cosine palettes are a gradient generation method — they produce the values
- **flow-fields**: Map flow field values to cosine palette colors — continuous color along paths
- **domain-warping**: Warp the t parameter before palette lookup for richer, more organic color variation
- **fbm-noise**: Use FBM output as t input — multi-octave noise drives multi-hue color

**Creates tension with:**
- posterize-quantization: Cosine palettes are smooth; posterize quantizes. The tension can be interesting — smooth palette snapped to bands.
- color-palettes: Both define color strategy. Use cosine for algorithmic variation, hand-picked for curated harmony.

**Medium fit:** gouache-layers, woven-textile, oil-impasto

**Explore from here:**
- If you like procedural color → also look at hsb-hsl-color for hue rotation approaches
- If you want palette animation → animate cosine coefficients over time with temporal-animation
- To invent something new → try different cosine palettes per composition zone via spatial-partitioning

## Art Blocks examples
- Watercolor Dreams by Numbersinmotion
- Anticyclone by William Mapan
- Meridian by Matt DesLauriers
