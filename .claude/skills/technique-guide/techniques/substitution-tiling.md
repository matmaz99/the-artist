# Substitution Tiling

## What it looks like
Aperiodic patterns that never repeat—like Penrose tilings. Complex, organic-looking tesselations with self-similar structure at different scales.

## How it works  
Start with seed tiles, apply substitution rules that replace each tile with a cluster of smaller tiles. Iterate to refine. Tiles have specific shapes and matching rules.

## Parameters
- **tile types**: shapes with substitution rules
- **iterations**: refinement levels
- **matching rules**: which edges connect

## Minimal p5.js sketch
```javascript
// Simplified substitution tiling
let tiles = [];

function setup() {
  createCanvas(400, 400);
  noLoop();
  
  // Start with one large tile
  tiles.push({x: 200, y: 200, size: 100, type: 0});
  
  // Subdivide
  for (let iter = 0; iter < 3; iter++) {
    let newTiles = [];
    for (let t of tiles) {
      // Substitute: one tile becomes 3 smaller tiles
      let s = t.size / 2;
      newTiles.push({x: t.x - s/2, y: t.y, size: s, type: (t.type + 1) % 2});
      newTiles.push({x: t.x + s/2, y: t.y - s/2, size: s, type: t.type});
      newTiles.push({x: t.x + s/2, y: t.y + s/2, size: s, type: (t.type + 1) % 2});
    }
    tiles = newTiles;
  }
}

function draw() {
  background(255);
  for (let t of tiles) {
    fill(t.type === 0 ? color(100, 150, 255) : color(255, 150, 100));
    stroke(0);
    rect(t.x - t.size/2, t.y - t.size/2, t.size, t.size);
  }
}
```

## Combinations

**Typical role:** structure — creates aperiodic, never-repeating tessellation patterns

**Works beautifully with:**
- **color-palettes**: Color tile types for visual distinction — each tile shape gets a palette role
- **hyperbolic-geometry**: Tilings in curved space for mind-bending infinite patterns
- **symmetry-mirroring**: Tiling symmetry groups create stunning repeating compositions
- **texture-synthesis**: Add surface texture to tiles for material feel — stone, wood, fabric

**Creates tension with:**
- flow-fields: Tilings are static structures; flow wants movement. Use flow to deform tile edges slightly.
- erode-dilate: Clean tile boundaries define the pattern — erosion can destroy readability.

**Medium fit:** woven-textile, ceramic-glaze

**Explore from here:**
- If you like non-repeating patterns → also look at voronoi-tessellation for organic tessellation
- If you want simpler tilings → try truchet-tiles for 2-state tile patterns
- To invent something new → try substitution tilings where tile interior is filled with reaction-diffusion patterns

## Art Blocks examples
- while true by Lars Wander
- while true (fabric) by Lars Wander
