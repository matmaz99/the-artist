# Stroke Hatching

## What it looks like
Dense parallel lines filling a region, wobbling slightly like pen strokes drawn freehand. The lines follow the contour of shapes, giving a cross-hatching or engraving quality. Areas feel hand-shaded rather than digitally filled.

## How it works
A shape is filled with evenly spaced parallel lines at a given angle. Each line is clipped to the shape boundary. Perlin noise displaces each point along the line perpendicular to the stroke direction, breaking up the mechanical regularity. Multiple hatching passes at different angles create cross-hatching. Line spacing controls perceived darkness.

## Parameters
- **spacing**: distance between parallel strokes
- **angle**: direction of hatching lines
- **noise amplitude**: how much lines wobble
- **noise frequency**: scale of the displacement noise

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(245);
  stroke(30);
  strokeWeight(0.8);
  noFill();

  let cx = 200, cy = 200, r = 140;
  let spacing = 4;
  let angle = PI / 6;

  for (let d = -r; d < r; d += spacing) {
    let along = createVector(cos(angle), sin(angle));
    let perp = createVector(-sin(angle), cos(angle));
    let base = createVector(cx + perp.x * d, cy + perp.y * d);

    beginShape();
    for (let t = -r; t <= r; t += 3) {
      let px = base.x + along.x * t;
      let py = base.y + along.y * t;
      let dx = dist(px, py, cx, cy);
      if (dx < r) {
        let n = noise(px * 0.02, py * 0.02) * 6 - 3;
        vertex(px + perp.x * n, py + perp.y * n);
      }
    }
    endShape();
  }
}
```

## Combinations

**Typical role:** detail — adds surface texture and tonal value through parallel line marks

**Works beautifully with:**
- **flow-fields**: Hatch perpendicular to flow direction for cross-contour texture
- **polygon-operations**: Fill irregular shapes with hatching instead of flat color
- **fat-line-stroke**: Hatch inside thick calligraphic strokes for printmaking feel
- **line-drawing**: Hatching is a natural extension of line-based rendering — systematic line fills

**Creates tension with:**
- texture-synthesis: Both add surface detail — using both risks visual noise. Pick one or keep one very subtle.
- gradient-systems: Hatching builds tone through line density; gradients through color. They can coexist if hatching density follows gradient value.

**Medium fit:** fine-pencil, etching-printmaking, charcoal-conte

**Explore from here:**
- If you like the linear quality → also look at line-drawing, ghost-stroke-doubling
- If you want denser tone → combine with erode-dilate for ink-bleed hatching
- To invent something new → try hatching that follows a flow field instead of parallel lines

## Art Blocks examples
- Fidenza by Tyler Hobbs
- Memories of Qilin by Emily Xie
- 923 EMPTY ROOMS by Casey REAS
