# Spatial Partitioning

## What it looks like
Efficiency structure—not directly visible but enables fast collision detection, neighbor searches, and culling for dense scenes.

## How it works  
Divide space into grid cells or tree structure (quadtree in 2D, octree in 3D). Objects belong to cells. Queries only check relevant cells, dramatically speeding up spatial operations.

## Parameters
- **cell size**: subdivision granularity
- **max depth**: tree depth limit
- **max objects per cell**: when to subdivide

## Minimal p5.js sketch
```javascript
// Quadtree visualization
class Quadtree {
  constructor(bounds, capacity) {
    this.bounds = bounds; // {x, y, w, h}
    this.capacity = capacity;
    this.points = [];
    this.divided = false;
  }
  
  insert(point) {
    if (this.points.length < this.capacity) {
      this.points.push(point);
      return true;
    }
    
    if (!this.divided) this.subdivide();
    // Insert into children (simplified)
    return true;
  }
  
  subdivide() {
    this.divided = true;
    // Create 4 child quadrants (code omitted for brevity)
  }
  
  show() {
    stroke(255);
    noFill();
    rect(this.bounds.x, this.bounds.y, this.bounds.w, this.bounds.h);
    for (let p of this.points) {
      point(p.x, p.y);
    }
  }
}

let qt;
function setup() {
  createCanvas(400, 400);
  qt = new Quadtree({x: 0, y: 0, w: width, h: height}, 4);
  for (let i = 0; i < 100; i++) {
    qt.insert({x: random(width), y: random(height)});
  }
  noLoop();
}

function draw() {
  background(0);
  qt.show();
}
```

## Combinations

**Typical role:** utility / optimization — divides space for efficient queries and collision detection

**Works beautifully with:**
- **particle-systems**: Fast collision checks between thousands of particles
- **circle-packing**: Efficient overlap testing during packing iterations
- **noise-density-scatter**: Efficient spatial queries for large-scale element placement
- **voronoi-tessellation**: Spatial trees accelerate nearest-neighbor queries for Voronoi

**Creates tension with:**
- flow-fields: Spatial partitioning is static; particles in flow move constantly. Use dynamic partitioning or rebuild each frame.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like spatial organization → also look at grid-layout for visual spatial structure
- If you want visible partitioning → render the tree structure itself as visual art
- To invent something new → try quad-tree subdivision as both optimization AND visual composition

## Art Blocks examples
- Ancient Courses of Fictional Rivers by Robert Hodgin
- Dipolar by Junia Farquhar
- Spaghetti Bones by Joshua Bagley
