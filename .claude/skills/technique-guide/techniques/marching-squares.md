# Marching Algorithms

## What it looks like
Smooth contour lines through scalar fields. Topographic-looking curves that trace level sets.

## How it works  
Sample field at grid vertices. For each cell, use the 4 corner values to determine contour configuration (16 cases). Draw line segments connecting edges based on threshold.

## Parameters
- **threshold**: contour level
- **interpolation**: linear or cubic edge positions
- **grid resolution**: sampling density

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  background(255);
  
  let res = 20;
  stroke(0);
  noFill();
  
  // Simple marching squares
  for (let x = 0; x < width - res; x += res) {
    for (let y = 0; y < height - res; y += res) {
      let a = noise(x * 0.01, y * 0.01);
      let b = noise((x + res) * 0.01, y * 0.01);
      let c = noise((x + res) * 0.01, (y + res) * 0.01);
      let d = noise(x * 0.01, (y + res) * 0.01);
      
      let threshold = 0.5;
      let config = 0;
      if (a > threshold) config += 1;
      if (b > threshold) config += 2;
      if (c > threshold) config += 4;
      if (d > threshold) config += 8;
      
      // Draw based on config (simplified)
      if (config === 1 || config === 14) {
        line(x, y + res/2, x + res/2, y + res);
      } else if (config === 7 || config === 8) {
        line(x, y + res/2, x + res/2, y);
      }
      // ... (15 more cases in full implementation)
    }
  }
}
```

## Combinations

**Typical role:** extraction — pulls contour lines from scalar fields for topographic clarity

**Works beautifully with:**
- **perlin-simplex-noise**: Generate the scalar field that marching squares extracts contours from
- **signed-distance-fields**: Extract smooth contours from SDF boundaries
- **fbm-noise**: Multi-octave noise creates rich, complex contour patterns — topographic maps
- **posterize-quantization**: Quantize the field first, then extract boundaries between quantized levels

**Creates tension with:**
- flow-fields: Contour lines cross flow directions — they're perpendicular to the gradient. Can create interesting interference patterns.

**Medium fit:** etching-printmaking

**Explore from here:**
- If you like contour extraction → also look at signed-distance-fields for smooth boundaries
- If you want filled regions → combine with posterize-quantization for flat-fill between contours
- To invent something new → try marching squares on the distance field of a voronoi-tessellation

## Art Blocks examples
- Ancient Courses of Fictional Rivers by Robert Hodgin
- Inspirals by radix
