# Line Drawing Systems

## What it looks like
Artwork built from lines—scribbles, hatching, contours, or geometric line art. From sketchy to precise, lines define form and texture.

## How it works  
Connect points with lines, vary strokeWeight, use algorithms like scribble (offsetting lines), hatching (parallel lines), or contouring (following shapes). Can be straight, curved, or noise-driven.

## Parameters
- **stroke weight**: line thickness
- **density**: spacing between lines
- **style**: straight, curved, rough

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(255);
  noFill();
  stroke(0);
}

function draw() {
  // Scribble effect
  let x = mouseX + random(-5, 5);
  let y = mouseY + random(-5, 5);
  let px = pmouseX + random(-5, 5);
  let py = pmouseY + random(-5, 5);
  
  strokeWeight(2);
  line(px, py, x, y);
}
```

## Combinations

**Typical role:** mark / foundation — builds imagery from individual line marks

**Works beautifully with:**
- **flow-fields**: Lines follow field vectors — every line has a direction and purpose
- **stroke-hatching**: Hatching is parallel line fills — the systematic variant of line drawing
- **curve-smoothing**: Smooth drawn lines for fluid, calligraphic quality
- **ghost-stroke-doubling**: Ghost echoes behind every line add hand-drawn warmth

**Creates tension with:**
- alpha-spatter: Lines are precise; spatter is chaotic. Together they create a wonderful inked-and-splattered look — controlled chaos.
- gradient-systems: Lines build tone through density; gradients through color. Use gradients for background, lines for subject.

**Medium fit:** fine-pencil, ink-on-paper, etching-printmaking

**Explore from here:**
- If you like line work → also look at fat-line-stroke for thicker variants
- If you want more texture → combine with stroke-hatching for filled regions
- To invent something new → try lines whose thickness responds to the distance from a signed-distance-field boundary

## Art Blocks examples
- Bent by ippsketch
- Dipolar by Junia Farquhar
- Elevated Deconstructions by luxpris
- Fidenza by Tyler Hobbs
- Ink by Iskra Velitchkova
