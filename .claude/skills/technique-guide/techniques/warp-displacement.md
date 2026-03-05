# Warp Displacement

## What it looks like
Structured geometry that has been bent, twisted, or folded through space. Regular grids become undulating waves, twisted spirals, folded fabric, or perspective-projected planes. The underlying regularity is still visible but the transformation creates dramatic visual tension between order and distortion.

## How it works
Before drawing any point, its coordinates are passed through a warp function that returns new coordinates. Common warp functions: **Wave** (sinusoidal displacement), **Twist** (angle proportional to distance from center), **Fold** (mirror coordinates around an axis), **Perspective** (divide by z for depth foreshortening). Multiple warps can be chained. The same grid drawn with different warps produces radically different compositions.

## Parameters
- **warp type**: wave, twist, fold, perspective, or custom
- **warp strength**: amplitude of the displacement
- **warp frequency**: for periodic warps like wave
- **warp center**: origin point for radial warps like twist

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(245);
  stroke(30);
  strokeWeight(0.8);
  noFill();

  let spacing = 15;
  let strength = 40;
  let freq = 0.015;

  // draw warped horizontal lines
  for (let y = spacing; y < height; y += spacing) {
    beginShape();
    for (let x = 0; x <= width; x += 3) {
      // twist warp: rotate point around center
      let cx = x - width / 2, cy = y - height / 2;
      let d = sqrt(cx * cx + cy * cy);
      let angle = atan2(cy, cx) + d * 0.008;
      let wx = width / 2 + cos(angle) * d;
      let wy = height / 2 + sin(angle) * d;
      // wave warp on top
      wy += sin(wx * freq) * strength * (d / 200);
      vertex(wx, wy);
    }
    endShape();
  }
}
```

## Combinations

**Typical role:** distortion — bends and folds structured geometry through space

**Works beautifully with:**
- **grid-layout**: Regular grids are the classic input — grid + warp = melting structure
- **flow-fields**: Flow-based warping as an alternative to analytic distortion functions
- **domain-warping**: Noise-based coordinate distortion — warp displacement is the spatial variant
- **perlin-simplex-noise**: Noise drives displacement amount and direction organically

**Creates tension with:**
- signed-distance-fields: Warping distorts SDF distances — breaks mathematical guarantees. Apply warp before SDF evaluation.
- truchet-tiles: Warping breaks tile connections — interesting if subtle, destructive if strong.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like spatial distortion → also look at domain-warping for coordinate-space distortion
- If you want subtler effect → use very low warp amplitude to just breathe life into rigid geometry
- To invent something new → try displacement that varies over time for breathing, pulsing forms

## Art Blocks examples
- Edifice by Ben Kovach
- Hyperhash by Beervangeer
- Singularity by Hideki Tsukamoto
