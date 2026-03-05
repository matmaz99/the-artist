# Fat Line Stroke

## What it looks like
Thick, calligraphic ribbons that taper at their ends like brush strokes or marker trails. The lines have weight and presence, with smooth width variation along their length giving a hand-drawn quality.

## How it works
A thin path (polyline or curve) is converted to a filled polygon by computing perpendicular offsets at each point. At each vertex, the normal vector is calculated and two offset points are placed on either side at a distance controlled by a width function. The width tapers near the start and end using a sine or smoothstep envelope. The offset points form a closed polygon that gets filled.

## Parameters
- **base width**: maximum stroke thickness at the center
- **taper function**: how width falls off at endpoints (sine, smoothstep, linear)
- **path resolution**: number of sample points along the curve
- **cap style**: round, flat, or pointed ends

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(245);
  noStroke();
  fill(30);

  let pts = [];
  for (let i = 0; i < 40; i++) {
    let t = i / 39;
    let x = lerp(60, 340, t) + sin(t * 5) * 40;
    let y = 200 + cos(t * 3) * 60;
    pts.push(createVector(x, y));
  }

  let maxW = 12;
  beginShape();
  for (let i = 0; i < pts.length; i++) {
    let t = i / (pts.length - 1);
    let w = maxW * sin(t * PI);
    let next = pts[min(i + 1, pts.length - 1)];
    let dir = p5.Vector.sub(next, pts[i]).normalize();
    let nx = -dir.y * w, ny = dir.x * w;
    vertex(pts[i].x + nx, pts[i].y + ny);
  }
  for (let i = pts.length - 1; i >= 0; i--) {
    let t = i / (pts.length - 1);
    let w = maxW * sin(t * PI);
    let next = pts[min(i + 1, pts.length - 1)];
    let dir = p5.Vector.sub(next, pts[i]).normalize();
    let nx = -dir.y * w, ny = dir.x * w;
    vertex(pts[i].x - nx, pts[i].y - ny);
  }
  endShape(CLOSE);
}
```

## Combinations

**Typical role:** mark / form — creates thick calligraphic ribbons with body and taper

**Works beautifully with:**
- **flow-fields**: Fat strokes following vector fields create Fidenza-like ribbons and currents
- **bezier-curves**: Smooth underlying paths for the stroke centerline — Bezier gives grace, fat-line gives weight
- **weighted-random**: Varying stroke width and taper per element for natural calligraphic variety
- **layered-composition**: Thick strokes at different layers create depth like overlapping paint ribbons

**Creates tension with:**
- stroke-hatching: Both are line-based marks but want different densities. Fat strokes are singular; hatching is many thin lines. Layer them — fat over hatch.
- grid-layout: Organic strokes fight grid containment. Interesting when strokes are constrained to grid channels.

**Medium fit:** gouache-layers, charcoal-conte, oil-impasto, ink-on-paper

**Explore from here:**
- If you like thick marks → also look at line-drawing for thinner variants
- If you want more body → combine with texture-synthesis for visible brush bristle texture
- To invent something new → try fat strokes whose width responds to audio-reactive input

## Art Blocks examples
- Fidenza by Tyler Hobbs
- Elevated Deconstructions by luxpris
- Strands of Solitude by William Tan
