# Posterize Quantization

## What it looks like
Smooth gradients reduced to flat bands of color with organic, contour-like boundaries between them. The effect resembles screen-printed layers, topographic maps, or risograph prints. Transitions are abrupt rather than smooth.

## How it works
A continuous value field (usually noise) is quantized by multiplying by the number of desired levels, flooring the result, then dividing back. `floor(value * levels) / levels` snaps continuous values to discrete steps. Each step maps to a distinct color. The boundaries between steps follow the natural contours of the noise field, creating organic shapes despite the hard color transitions.

## Parameters
- **levels**: number of discrete color steps (3-8 typical)
- **noise scale**: controls the size of contour shapes
- **palette**: colors assigned to each level
- **edge smoothing**: optional slight feather at boundaries

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noStroke();
  let levels = 5;
  let pal = ['#1a1a2e', '#16213e', '#0f3460', '#e94560', '#f5e6ca'];
  let step = 4;

  for (let x = 0; x < width; x += step) {
    for (let y = 0; y < height; y += step) {
      let n = noise(x * 0.008, y * 0.008);
      let q = floor(n * levels) / levels;
      let idx = floor(q * levels);
      fill(pal[constrain(idx, 0, pal.length - 1)]);
      rect(x, y, step, step);
    }
  }
}
```

## Combinations

**Typical role:** simplification — reduces continuous values to discrete bands for graphic clarity

**Works beautifully with:**
- **perlin-simplex-noise**: The continuous field that gets quantized — noise becomes flat color zones
- **fbm-noise**: Multi-octave noise creates richer contour shapes when quantized
- **marching-squares**: Extract exact boundary curves between quantized levels
- **color-palettes**: Map each quantized level to a curated palette color

**Creates tension with:**
- gradient-systems: Gradients want smooth transitions; posterize wants steps. The tension creates topographic elevation maps.
- ghost-stroke-doubling: Ghosts are subtle transparency; posterize eliminates subtlety. One or the other.

**Medium fit:** gouache-layers, spray-paint, etching-printmaking, ceramic-glaze

**Explore from here:**
- If you like flat color areas → also look at voronoi-tessellation for cell-based flat fills
- If you want printed feel → combine with stroke-hatching inside quantized regions
- To invent something new → try adaptive posterization where the number of levels varies across the canvas with fbm-noise

## Art Blocks examples
- INK by Iskra Velitchkova
- Shards by Alexis Andre
- Trossets by Anna Carreras
