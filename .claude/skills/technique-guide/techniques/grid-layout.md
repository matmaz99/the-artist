# Grid-Based Layout

## What it looks like
Orderly arrangements of cells, tiles, or subdivisions. You see structure and repetition, from regular grids to recursively split spaces. The composition feels architectural and organized.

## How it works  
The canvas divides into rows and columns, or cells split recursively. Each cell can contain different content. Simple grids use nested loops, while complex systems track cell boundaries and split them based on rules.

## Parameters
- **columns & rows**: grid dimensions
- **cell size**: dimensions of each unit
- **padding/margin**: spacing between cells

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  background(240);
  let cols = 8, rows = 8;
  let cellW = width / cols;
  let cellH = height / rows;
  
  for (let i = 0; i < cols; i++) {
    for (let j = 0; j < rows; j++) {
      let x = i * cellW;
      let y = j * cellH;
      fill(random() > 0.5 ? 0 : 255);
      rect(x, y, cellW, cellH);
    }
  }
}
```

## Combinations

**Typical role:** structure — provides regular spatial organization for elements

**Works beautifully with:**
- **recursive-subdivision**: Grids split into finer grids — nested structure at multiple scales
- **truchet-tiles**: Each grid cell contains a rotated tile — the grid enables the pattern
- **color-palettes**: Color cells by position, index, or random palette sampling
- **seigaiha-wave-pattern**: Grid provides the brick-offset arrangement for wave arcs

**Creates tension with:**
- flow-fields: Grid wants order; flow wants organic movement. Use flow inside cells or to deform the grid slightly.
- differential-growth: Growth breaks grids. Let growth happen between grid lines, or start growth from grid intersections.

**Medium fit:** woven-textile

**Explore from here:**
- If you like regular structure → also look at apparatus-grid for Mondrian-like subdivision
- If you want to break the grid → add warp-displacement for subtle bending
- To invent something new → try grids where cell size varies with fbm-noise

## Art Blocks examples
- Colorspace by Tabor Robak
- Construction Token by Jeff Davis
- Dynamic Slices by pxlq
- Trichro-matic by MountVitruvius
- Act of Emotion by Kelly Milligan
