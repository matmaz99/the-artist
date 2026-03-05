# Truchet Tiles

## What it looks like
Infinite maze-like patterns from simple rotated tiles. Organic, flowing connections that never repeat the same way.

## How it works  
Each grid cell contains one of a small set of tile patterns, randomly rotated. Tiles are designed to connect seamlessly. Produces complex labyrinths from simple elements.

## Parameters
- **tile designs**: arc, line, or shape patterns
- **rotation**: 0°, 90°, 180°, 270°
- **grid density**: tile size

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  background(255);
  let tileSize = 40;
  
  for (let x = 0; x < width; x += tileSize) {
    for (let y = 0; y < height; y += tileSize) {
      push();
      translate(x, y);
      rotate(floor(random(4)) * HALF_PI);
      
      // Draw arc tile
      noFill();
      stroke(0);
      strokeWeight(2);
      arc(0, 0, tileSize, tileSize, 0, HALF_PI);
      arc(tileSize, tileSize, tileSize, tileSize, PI, PI + HALF_PI);
      
      pop();
    }
  }
}
```

## Combinations

**Typical role:** pattern — creates maze-like connected patterns from simple rotated tiles

**Works beautifully with:**
- **grid-layout**: Truchet requires a grid — the tile rotation happens on grid cells
- **color-palettes**: Color tiles for visual richness — each rotation state can have unique colors
- **symmetry-mirroring**: Truchet patterns naturally create symmetric arrangements
- **seigaiha-wave-pattern**: Similar tile-based logic — can be intermixed for pattern variety

**Creates tension with:**
- flow-fields: Truchet is discrete (per-tile); flow is continuous. Interesting if flow determines tile rotation angle.
- erode-dilate: Clean tile connections define the pattern — erosion breaks the maze. Subtle erosion can age it nicely.

**Medium fit:** woven-textile, ceramic-glaze

**Explore from here:**
- If you like tile patterns → also look at substitution-tiling for aperiodic alternatives
- If you want more connection types → try multi-state Truchet tiles with curves and straight segments
- To invent something new → try 3D Truchet on an isometric-projection grid

## Art Blocks examples
- Sudfah by Melissa Wiederrecht
- Trossets by Anna Carreras
