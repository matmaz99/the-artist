# Seigaiha Wave Pattern

## What it looks like
Overlapping rows of concentric half-circle arcs in a brick-offset arrangement. The classic Japanese decorative motif resembling ocean waves or fish scales. Dense, rhythmic, and meditative when covering a full surface.

## How it works
A grid of circles is arranged with brick-offset (every other row shifted by half a cell width). At each grid point, multiple concentric arcs are drawn from 0 to PI (half circles). The arcs overlap their neighbors, creating the characteristic layered wave appearance. Each row partially occludes the row behind it, so rows are drawn back to front.

## Parameters
- **cell size**: diameter of each wave unit
- **arc count**: number of concentric arcs per cell
- **row overlap**: vertical spacing between rows (typically half the radius)
- **palette**: colors assigned to arcs or rows

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(245);
  noFill();
  strokeWeight(1.2);

  let r = 30;
  let cols = ceil(width / r) + 1;
  let rows = ceil(height / (r * 0.5)) + 1;
  let pal = ['#264653', '#2a9d8f', '#e9c46a', '#f4a261', '#e76f51'];

  for (let row = rows; row >= 0; row--) {
    let offsetX = (row % 2) * r * 0.5;
    for (let col = -1; col < cols; col++) {
      let cx = col * r + offsetX;
      let cy = row * r * 0.5;
      for (let i = 5; i >= 1; i--) {
        stroke(pal[i % pal.length]);
        arc(cx, cy, (r / 5) * i * 2, (r / 5) * i * 2, PI, TWO_PI);
      }
    }
  }
}
```

## Combinations

**Typical role:** motif / decoration — creates the classic overlapping wave-arc pattern

**Works beautifully with:**
- **grid-layout**: The underlying brick-offset grid drives placement of wave arcs
- **truchet-tiles**: Similar tile-based pattern logic — can be intermixed for variety
- **texture-synthesis**: Layering seigaiha with noise creates aged textile quality
- **color-palettes**: Color arcs by row, column, or depth for rich decorative effect

**Creates tension with:**
- flow-fields: Seigaiha is a rigid repeating pattern; flow wants variation. Use flow to subtly shift arc centers.
- erode-dilate: Clean arc lines are the essence of seigaiha — erosion can destroy readability. Use very subtly for aged feel.

**Medium fit:** woven-textile, ceramic-glaze

**Explore from here:**
- If you like decorative patterns → also look at truchet-tiles, concentric-ring-fill
- If you want variation → modulate arc count per cell with noise-density-scatter
- To invent something new → try seigaiha where arc radius varies with perlin-simplex-noise for breathing waves

## Art Blocks examples
- Memories of Qilin by Emily Xie
- Silk and Storms by Emily Xie
- Eastern Blocks by Alexis Andre
