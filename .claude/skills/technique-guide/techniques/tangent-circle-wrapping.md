# Tangent Circle Wrapping

## What it looks like
Taut bands or strings stretched between circles, like rubber bands wrapped around pegs. The lines follow the exact tangent points where they touch each circle, creating elegant bridge curves between circular forms. The result resembles string art or technical drawing.

## How it works
For two circles with centers (x1,y1), (x2,y2) and radii r1, r2, compute the external tangent lines. The tangent touch points are found by calculating the angle between centers, then offsetting by asin((r1-r2)/d) for external tangents (where d is center distance). Lines connect the tangent points on each circle. For multiple circles, connect each pair to build a web of wrapping bands.

## Parameters
- **circle count**: number of pegs/circles
- **circle radii**: size range of circles
- **band width**: thickness of the connecting strokes
- **wrap type**: external tangent, internal tangent, or both

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(245);
  stroke(30);
  strokeWeight(1.5);
  noFill();

  let circles = [];
  for (let i = 0; i < 6; i++) {
    circles.push({ x: random(80, 320), y: random(80, 320), r: random(15, 45) });
  }

  for (let c of circles) ellipse(c.x, c.y, c.r * 2);

  for (let i = 0; i < circles.length; i++) {
    for (let j = i + 1; j < circles.length; j++) {
      let a = circles[i], b = circles[j];
      let d = dist(a.x, a.y, b.x, b.y);
      if (d < a.r + b.r) continue;
      let angle = atan2(b.y - a.y, b.x - a.x);
      let offset = asin((a.r - b.r) / d);

      for (let s of [-1, 1]) {
        let ta = angle + HALF_PI * s + offset;
        let tb = angle + HALF_PI * s + offset;
        line(
          a.x + cos(ta) * a.r, a.y + sin(ta) * a.r,
          b.x + cos(tb) * b.r, b.y + sin(tb) * b.r
        );
      }
    }
  }
}
```

## Combinations

**Typical role:** form — creates taut bands stretched between circles like rubber bands on pegs

**Works beautifully with:**
- **circle-packing**: Packed circles as pegs for the wrapping bands — the natural layout for tangent circles
- **bezier-curves**: Curved bands instead of straight tangent lines for more organic wrapping
- **polygon-operations**: Clip or intersect wrapping regions for complex band interactions
- **color-palettes**: Color each band or region differently for visual separation

**Creates tension with:**
- flow-fields: Tangent lines are geometrically determined; flow wants organic curves. Use flow to subtly deform the bands.

**Medium fit:** ink-on-paper

**Explore from here:**
- If you like geometric string art → also look at bezier-curves for more control
- If you want more organic wrapping → combine with curve-smoothing for smoother band paths
- To invent something new → try tangent wrapping where the circles drift with physics-simulation

## Art Blocks examples
- Ringers by Dmitri Cherniak
- Geometry Runners by Rich Lord
- Network Effect by Casey REAS
