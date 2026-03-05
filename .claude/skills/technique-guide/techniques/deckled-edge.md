# Deckled Edge

## What it looks like
Ragged, torn-paper borders instead of clean straight edges. The boundary of the artwork or a shape looks like handmade paper torn from a mould, with irregular fibers and soft undulations along the edge.

## How it works
Each straight edge of a rectangle is replaced by a noise-displaced curve. Walk along the edge at small intervals, displacing each point perpendicular to the edge using layered Perlin noise (low frequency for broad waves, high frequency for fiber-scale jaggedness). The displaced points form the new border polygon. Small random strokes near the boundary simulate loose paper fibers.

## Parameters
- **noise amplitude**: how far the edge deviates from straight
- **noise frequency**: scale of the undulation
- **fiber density**: number of small hair-like marks at the boundary
- **octaves**: noise layers (low = gentle waves, high = rough tear)

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(220);
  fill(250, 245, 235);
  noStroke();

  let margin = 50, steps = 200;
  let amp = 12;

  beginShape();
  for (let i = 0; i <= steps; i++) {
    let t = i / steps;
    vertex(lerp(margin, width - margin, t) + noise(t * 3, 0) * amp - amp / 2, margin + noise(t * 3, 10) * amp - amp / 2);
  }
  for (let i = 0; i <= steps; i++) {
    let t = i / steps;
    vertex(width - margin + noise(t * 3, 20) * amp - amp / 2, lerp(margin, height - margin, t) + noise(t * 3, 30) * amp - amp / 2);
  }
  for (let i = steps; i >= 0; i--) {
    let t = i / steps;
    vertex(lerp(margin, width - margin, t) + noise(t * 3, 40) * amp - amp / 2, height - margin + noise(t * 3, 50) * amp - amp / 2);
  }
  for (let i = steps; i >= 0; i--) {
    let t = i / steps;
    vertex(margin + noise(t * 3, 60) * amp - amp / 2, lerp(margin, height - margin, t) + noise(t * 3, 70) * amp - amp / 2);
  }
  endShape(CLOSE);

  stroke(180);
  strokeWeight(0.5);
  for (let i = 0; i < 300; i++) {
    let side = floor(random(4));
    let t = random();
    let x, y;
    if (side === 0) { x = lerp(margin, width - margin, t); y = margin; }
    else if (side === 1) { x = width - margin; y = lerp(margin, height - margin, t); }
    else if (side === 2) { x = lerp(margin, width - margin, t); y = height - margin; }
    else { x = margin; y = lerp(margin, height - margin, t); }
    line(x, y, x + random(-6, 6), y + random(-6, 6));
  }
}
```

## Combinations

**Typical role:** framing / finish — adds torn-paper or ragged borders to the artwork

**Works beautifully with:**
- **texture-synthesis**: Paper texture inside the deckled boundary — the surface the painting lives on
- **layered-composition**: Torn paper edges between collage layers — each layer has its own ragged boundary
- **perlin-simplex-noise**: Drives the edge displacement — noise makes the tear pattern organic
- **stroke-hatching**: Hatching that fades near deckled edges creates a vignette-like focus

**Creates tension with:**
- grid-layout: Clean grid edges fight ragged borders. Use deckled edge on the outermost frame only, not on internal grid lines.

**Medium fit:** watercolor-wash, etching-printmaking, ink-on-paper, woven-textile

**Explore from here:**
- If you like handmade borders → also look at erode-dilate for ink-bleed edges
- If you want more frame presence → combine with a visible paper margin using texture-synthesis
- To invent something new → try deckled edges that follow the contour of internal shapes, not just the canvas boundary

## Art Blocks examples
- Memories of Qilin by Emily Xie
- Paper Armada by Kjetil Golid
- Rough Cuts by miquelcrespo
