# Curve Smoothing

## What it looks like
Rough paths become fluid curves. Jaggy lines turn into smooth, natural-looking contours.

## How it works  
Algorithms like Chaikin's corner-cutting or Bezier fitting take point sequences and generate smooth curves through or near them. Can also use low-pass filters on vertex positions.

## Parameters
- **iterations**: number of smoothing passes
- **tension**: how close curve follows original points
- **subdivision**: points added per smoothing

## Minimal p5.js sketch
```javascript
let points = [];

function setup() {
  createCanvas(400, 400);
  for (let i = 0; i < 10; i++) {
    points.push(createVector(random(width), random(height)));
  }
}

function draw() {
  background(255);
  
  // Original jagged path
  stroke(200, 0, 0);
  noFill();
  beginShape();
  for (let p of points) vertex(p.x, p.y);
  endShape();
  
  // Smoothed with curveVertex
  stroke(0);
  strokeWeight(2);
  beginShape();
  curveVertex(points[0].x, points[0].y);
  for (let p of points) curveVertex(p.x, p.y);
  curveVertex(points[points.length-1].x, points[points.length-1].y);
  endShape();
}
```

## Combinations

**Typical role:** refinement — turns rough paths into fluid, natural-looking curves

**Works beautifully with:**
- **flow-fields**: Smooth particle trails so they look drawn by hand rather than computed
- **line-drawing**: Smooth hand-drawn feel on any line-based rendering
- **differential-growth**: Smooth differential growth curves so they look like organic surfaces, not jagged polygons
- **bezier-curves**: Convert point sequences to smooth Bezier approximations

**Creates tension with:**
- stroke-hatching: Hatching benefits from slight irregularity — too much smoothing kills the hand-drawn quality.

**Medium fit:** fine-pencil, ink-on-paper

**Explore from here:**
- If you like smooth curves → also look at bezier-curves for precise control
- If you want selective smoothing → vary smoothing amount by speed or pressure for calligraphic feel
- To invent something new → try smoothing that preserves sharp corners while rounding gentle bends

## Art Blocks examples
- Apparitions by Aaron Penne
- Chromie Squiggle by Snowfro
- Spaghetti Bones by Joshua Bagley
