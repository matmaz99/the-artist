# Signed Distance Fields (SDF)

## What it looks like
Perfectly smooth 3D-looking shapes rendered in 2D. Circles, boxes, and organic blobs with anti-aliased edges and the ability to blend, subtract, or intersect.

## How it works  
For each pixel, calculate its distance to the nearest point on a shape. Positive values are outside, negative inside, zero on the edge. Use this to render with perfect curves and combine shapes using min/max operations.

## Parameters
- **primitive type**: sphere, box, torus, etc.
- **operations**: union, subtraction, intersection
- **smoothing**: blend radius for smooth booleans

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
      let px = (x - width/2) / 100;
      let py = (y - height/2) / 100;
      
      // Distance to circle center
      let d = sqrt(px*px + py*py) - 1.0;
      
      // Color based on distance
      let col = d < 0 ? 255 : 0;
      let idx = (x + y * width) * 4;
      pixels[idx] = col;
      pixels[idx + 1] = col;
      pixels[idx + 2] = col;
      pixels[idx + 3] = 255;
    }
  }
  updatePixels();
}
```

## Combinations

**Typical role:** form — defines shapes through distance functions for smooth, precise geometry

**Works beautifully with:**
- **ray-marching**: SDFs define 3D volumes that ray marching renders into visible forms
- **webgl-shaders**: GPU-accelerated SDF rendering for smooth, anti-aliased shapes in real-time
- **gradient-systems**: Map SDF distance values to color gradients — color radiates from boundaries
- **marching-squares**: Extract smooth contour lines from SDF boundaries

**Creates tension with:**
- erode-dilate: SDFs have mathematically perfect edges; erosion destroys that precision. Beautiful if intentional — weathered geometry.
- stroke-hatching: SDFs define area; hatching fills area with texture. They complement each other well.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like smooth shapes → also look at polygon-operations for combinatorial geometry
- If you want organic SDFs → combine with domain-warping to distort the distance field
- To invent something new → try SDF boolean operations animated over time — shapes that merge and split

## Art Blocks examples
- Bubble Blobby by Jason Ting
- Flux by Owen Moore
- Gumbo by Mathias Isaksen
- HyperHash by Beervangeer
- Skulptuur by Piter Pasma
