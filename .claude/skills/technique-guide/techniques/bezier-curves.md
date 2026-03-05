# Bezier Curves

## What it looks like
Smooth, elegant curves that flow naturally. Unlike straight lines or arcs, Bezier curves can create organic shapes and flowing paths with precise control.

## How it works  
Bezier curves use control points to define smooth paths. Cubic Beziers have start, end, and two control points. The curve is calculated by interpolating positions along the parameter t from 0 to 1.

## Parameters
- **control points**: positions that influence curve shape
- **segments**: curve resolution
- **tension**: how tightly curve follows controls

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(255);
  noFill();
  stroke(0);
  strokeWeight(2);
  
  let x1 = 50, y1 = 200;
  let x2 = 350, y2 = 200;
  let cx1 = mouseX, cy1 = 100;
  let cx2 = mouseX, cy2 = 300;
  
  bezier(x1, y1, cx1, cy1, cx2, cy2, x2, y2);
  
  // Show control points
  stroke(255, 0, 0);
  strokeWeight(6);
  point(cx1, cy1);
  point(cx2, cy2);
}
```

## Combinations

**Typical role:** form / path — defines smooth curved shapes and trajectories

**Works beautifully with:**
- **flow-fields**: Curves follow field directions — field gives intent, Bezier gives smoothness
- **line-drawing**: Build complex shapes from curves — Bezier is the precise variant of free-form lines
- **fat-line-stroke**: Smooth underlying paths for thick calligraphic strokes — Bezier centerline + variable width
- **curve-smoothing**: Post-process rough curves into clean Bezier approximations

**Creates tension with:**
- stroke-hatching: Hatching wants straight parallel lines; Bezier wants flowing curves. Use Bezier paths as hatching guides for a printmaking feel.

**Medium fit:** ink-on-paper, fine-pencil

**Explore from here:**
- If you like smooth paths → also look at curve-smoothing, flow-fields
- If you want more geometric → try combining with grid-layout for structured curve placement
- To invent something new → try Bezier curves whose control points drift with domain-warping

## Art Blocks examples
- Alan Ki Aankhen by Fahad Karim
- Ancient Courses of Fictional Rivers by Robert Hodgin
- entretiempos by Marcelo Soria-Rodríguez
- Fragments of an Infinite Field by Monica Rizzolli
- Genesis by DCA
