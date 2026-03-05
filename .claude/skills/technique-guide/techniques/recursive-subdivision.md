# Recursive Subdivision

## What it looks like
Nested rectangles or polygons that progressively split into smaller sections. You see hierarchical structure, like rooms dividing into smaller rooms. The pattern has depth and variation at different scales.

## How it works  
Start with a shape. Test if it should split (based on depth, size, or randomness). If yes, divide it into smaller shapes and repeat recursively. The process stops when shapes are too small or maximum depth is reached.

## Parameters
- **max depth**: subdivision levels
- **min size**: smallest cell dimension
- **split probability**: chance to subdivide
- **split ratio**: where to divide

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  background(255);
  subdivide(0, 0, width, height, 0);
}

function subdivide(x, y, w, h, depth) {
  stroke(0); noFill();
  rect(x, y, w, h);
  
  if (depth < 4 && w > 40 && h > 40 && random() > 0.3) {
    let split = random(0.3, 0.7);
    if (random() > 0.5) {
      subdivide(x, y, w * split, h, depth + 1);
      subdivide(x + w * split, y, w * (1 - split), h, depth + 1);
    } else {
      subdivide(x, y, w, h * split, depth + 1);
      subdivide(x, y + h * split, w, h * (1 - split), depth + 1);
    }
  }
}
```

## Combinations

**Typical role:** structure — creates nested spatial hierarchy through repeated splitting

**Works beautifully with:**
- **grid-layout**: Subdivisions within grid cells for multi-scale structure
- **color-palettes**: Each subdivision level gets a different color treatment
- **polygon-operations**: Clip subdivisions to non-rectangular boundaries
- **weighted-random**: Random subdivision ratios and split directions for organic variety

**Creates tension with:**
- flow-fields: Subdivision is axis-aligned; flow is organic. Use flow inside subdivided cells.
- differential-growth: Both create spatial hierarchy but through opposite means — mechanical vs organic. Interesting contrast.

**Medium fit:** woven-textile

**Explore from here:**
- If you like spatial hierarchy → also look at apparatus-grid for Mondrian-like blocks
- If you want organic subdivision → try voronoi-tessellation for non-rectangular splits
- To invent something new → try recursive subdivision where the split ratio is driven by fbm-noise

## Art Blocks examples
- Archetype by Kjetil Golid
- Dipolar by Junia Farquhar
- Trossets by Anna Carreras
- Cargo by Kim Asendorf
- Primitives by Aranda\Lasch
