# Polygon Operations

## What it looks like
Complex shapes created by cutting, merging, or intersecting polygons. Clean boolean operations that handle edge cases correctly—union creates combined shapes, intersection reveals overlaps, difference cuts holes.

## How it works  
Libraries like Clipper or martinez-polygon-clipping perform union, intersection, and difference operations. They handle self-intersecting polygons and holes. Algorithms trace edges, find intersection points, and build result polygons by determining which segments are inside/outside. The sweep line algorithm is commonly used for efficiency.

## Parameters
- **operation type**: union (combine), intersection (overlap), difference (subtract), XOR (symmetric difference)
- **fill rule**: even-odd or non-zero winding number
- **tolerance**: precision for intersection calculations

## Minimal p5.js sketch
```javascript
// Simplified polygon intersection visualization
// Real implementation would use martinez or clipper library

function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  background(255);
  
  // Polygon A
  fill(255, 0, 0, 100);
  stroke(255, 0, 0);
  beginShape();
  vertex(100, 100);
  vertex(250, 100);
  vertex(250, 250);
  vertex(100, 250);
  endShape(CLOSE);
  
  // Polygon B  
  fill(0, 0, 255, 100);
  stroke(0, 0, 255);
  beginShape();
  vertex(150, 150);
  vertex(300, 150);
  vertex(300, 300);
  vertex(150, 300);
  endShape(CLOSE);
  
  // Intersection region (manually computed for demo)
  fill(255, 0, 255, 200);
  stroke(0);
  strokeWeight(2);
  rect(150, 150, 100, 100);
  
  textSize(12);
  fill(0);
  noStroke();
  text('Union: combine both shapes', 10, 20);
  text('Intersection: purple overlap', 10, 40);
  text('Difference: A minus B', 10, 60);
}

// Real implementation:
// import martinez from 'martinez-polygon-clipping'
// let result = martinez.intersection(polyA, polyB)
```

## Combinations

**Typical role:** form — creates complex shapes by combining, cutting, or intersecting simpler ones

**Works beautifully with:**
- **recursive-subdivision**: Clip subdivisions to complex polygon boundaries
- **voronoi-tessellation**: Clip Voronoi cells to canvas bounds or mask regions
- **line-drawing**: Render clipped polygon edges as drawn lines
- **stroke-hatching**: Fill polygons with hatching instead of flat color for a printmaking feel

**Creates tension with:**
- flow-fields: Flow is continuous; polygon ops are hard-edged. Use polygon boundaries to constrain flow regions.

**Medium fit:** etching-printmaking

**Explore from here:**
- If you like boolean geometry → also look at signed-distance-fields for smooth boolean operations
- If you want softer edges → combine with erode-dilate to soften polygon boundaries
- To invent something new → try polygon intersection between voronoi cells and differential-growth boundaries

## Art Blocks examples
- Neural Sediments by Eko33
- ORI by James Merrill
- Dipolar by Junia Farquhar
