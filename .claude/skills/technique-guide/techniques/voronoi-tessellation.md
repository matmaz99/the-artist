# Voronoi Tessellation

## What it looks like
Organic cell patterns where each cell is closest to one seed point. Like cracked earth, giraffe spots, or stained glass.

## How it works  
Place seed points, then for each pixel find which seed is nearest. All pixels with same nearest seed form a cell. Can compute edges to draw cell boundaries.

## Parameters
- **point count**: number of cells
- **distance metric**: Euclidean, Manhattan, etc.
- **edge style**: cell outlines or fills

## Minimal p5.js sketch
```javascript
let points = [];

function setup() {
  createCanvas(400, 400);
  noLoop();
  
  for (let i = 0; i < 30; i++) {
    points.push(createVector(random(width), random(height)));
  }
}

function draw() {
  loadPixels();
  
  for (let x = 0; x < width; x++) {
    for (let y = 0; y < height; y++) {
      let minDist = Infinity;
      let closest = 0;
      
      for (let i = 0; i < points.length; i++) {
        let d = dist(x, y, points[i].x, points[i].y);
        if (d < minDist) {
          minDist = d;
          closest = i;
        }
      }
      
      let idx = (x + y * width) * 4;
      let hue = (closest * 30) % 255;
      pixels[idx] = hue;
      pixels[idx + 1] = hue;
      pixels[idx + 2] = hue;
      pixels[idx + 3] = 255;
    }
  }
  updatePixels();
}
```

## Combinations

**Typical role:** layout — divides space into organic cells based on seed point proximity

**Works beautifully with:**
- **circle-packing**: Voronoi cells around packed circles — dual representation of packing layout
- **color-palettes**: Color cells by index, area, neighbor count, or random palette sampling
- **noise-density-scatter**: Scatter Voronoi seeds in organic clusters for natural cell distribution
- **polygon-operations**: Clip Voronoi cells to canvas bounds or mask regions

**Creates tension with:**
- grid-layout: Voronoi is organic; grids are regular. Use grid points as Voronoi seeds for a semi-regular tessellation.
- symmetry-mirroring: Voronoi is inherently asymmetric. Mirror seed points for symmetric Voronoi.

**Medium fit:** ceramic-glaze

**Explore from here:**
- If you like organic cells → also look at recursive-subdivision for hierarchical splitting
- If you want smoother cells → apply curve-smoothing to cell boundaries
- To invent something new → try animated Voronoi where seeds drift with flow-fields over time

## Art Blocks examples
- Autology by steganon
