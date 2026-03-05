# Apparatus Grid

## What it looks like
Mondrian-like compositions of rectangles at various scales, but with organic irregularity. Some cells are tiny, others span many grid units. The result feels like an architectural plan or a circuit board with varied block sizes and occasional color fills.

## How it works
Start with a grid of cells. Iterate through each cell: with some probability it becomes a new standalone block; otherwise it tries to extend an existing block from the left or from above. This greedy growth algorithm produces rectangles of varied sizes without overlap. After the grid is resolved, each block is drawn with a random color from a palette or left empty. Border thickness and padding add structure.

## Parameters
- **grid columns/rows**: underlying cell resolution
- **extend probability**: chance a cell merges with neighbor (0.3-0.7)
- **fill probability**: chance a block gets a color vs stays empty
- **border weight**: thickness of cell outlines

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(245);
  let cols = 12, rows = 12;
  let cw = width / cols, ch = height / rows;
  let grid = Array.from({ length: rows }, () => Array(cols).fill(-1));
  let blocks = [];
  let id = 0;

  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (grid[r][c] >= 0) continue;
      let extL = c > 0 && random() < 0.4 && grid[r][c - 1] >= 0;
      let extU = r > 0 && random() < 0.4 && grid[r - 1][c] >= 0;
      if (extL) { grid[r][c] = grid[r][c - 1]; blocks[grid[r][c]].w++; }
      else if (extU) { grid[r][c] = grid[r - 1][c]; blocks[grid[r][c]].h++; }
      else { grid[r][c] = id; blocks.push({ c, r, w: 1, h: 1 }); id++; }
    }
  }

  let pal = ['#e63946', '#457b9d', '#f1faee', '#a8dadc', '#1d3557'];
  stroke(30);
  strokeWeight(2);
  for (let b of blocks) {
    fill(random() < 0.6 ? random(pal) : 245);
    rect(b.c * cw + 2, b.r * ch + 2, b.w * cw - 4, b.h * ch - 4);
  }
}
```

## Combinations

**Typical role:** structure — provides the compositional skeleton of irregular rectangles

**Works beautifully with:**
- **grid-layout**: The underlying regular grid that gets subdivided into apparatus blocks
- **recursive-subdivision**: Alternative or complementary subdivision strategy for richer nesting
- **weighted-random**: Controls merge probabilities for compositional variety in block sizes
- **cosine-gradient-palette**: Rich color fills within each block — gradients respect block boundaries

**Creates tension with:**
- flow-fields: Apparatus wants rigid rectangles; flow wants organic curves. Interesting but requires care — maybe flow only inside blocks.
- differential-growth: Organic growth fights geometric containment. Use one to modulate the other, not both at full strength.

**Medium fit:** woven-textile

**Explore from here:**
- If you like the grid structure → also look at grid-layout, recursive-subdivision, truchet-tiles
- If you want more organic feel → add warp-displacement to bend the grid slightly
- To invent something new → try apparatus blocks where each cell contains a different mark system

## Art Blocks examples
- Archetype by Kjetil Golid
- CENTURY by Casey REAS
- Primitives by Aranda/Lasch
