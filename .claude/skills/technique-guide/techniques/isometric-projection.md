# Isometric Projection

## What it looks like
3D-looking structures displayed in 2D with parallel projection. Buildings, landscapes, or grids that show depth without perspective distortion.

## How it works  
Transform 3D coordinates (x, y, z) to screen position using iso formulas: screenX = x - z, screenY = y + (x + z) / 2. Draw from back to front for proper layering.

## Parameters
- **tile size**: base grid unit
- **height scale**: vertical exaggeration
- **angle**: isometric angle (typically 30°)

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  background(220);
  translate(width/2, height/3);
  
  for (let x = 0; x < 5; x++) {
    for (let y = 0; y < 5; y++) {
      let h = noise(x, y) * 3;
      drawIsoBox(x, y, 0, h);
    }
  }
}

function drawIsoBox(x, y, z, h) {
  let tileW = 40;
  let isoX = (x - y) * tileW/2;
  let isoY = (x + y) * tileW/4 - z * tileW/2;
  
  // Top
  fill(200);
  quad(isoX, isoY - h*tileW/2,
       isoX + tileW/2, isoY + tileW/4 - h*tileW/2,
       isoX, isoY + tileW/2 - h*tileW/2,
       isoX - tileW/2, isoY + tileW/4 - h*tileW/2);
  
  // Right face
  fill(150);
  quad(isoX, isoY - h*tileW/2,
       isoX + tileW/2, isoY + tileW/4 - h*tileW/2,
       isoX + tileW/2, isoY + tileW/4,
       isoX, isoY + tileW/2);
  
  // Left face
  fill(100);
  quad(isoX, isoY - h*tileW/2,
       isoX - tileW/2, isoY + tileW/4 - h*tileW/2,
       isoX - tileW/2, isoY + tileW/4,
       isoX, isoY + tileW/2);
}
```

## Combinations

**Typical role:** perspective — gives flat 2D elements a 3D architectural look

**Works beautifully with:**
- **grid-layout**: Isometric grids of tiles for city-like or crystal-like compositions
- **perlin-simplex-noise**: Height maps for terrain — noise drives block height in isometric view
- **color-palettes**: Face-specific coloring — top face light, left face mid, right face dark
- **recursive-subdivision**: Nested isometric blocks for fractal architecture

**Creates tension with:**
- flow-fields: Flow is inherently 2D; isometric wants 3D feel. Use flow for color or texture on isometric faces.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like 3D structure → also look at ray-marching for true volumetric rendering
- If you want more organic shapes → combine with voronoi-tessellation for irregular isometric cells
- To invent something new → try isometric blocks where each face shows a different technique

## Art Blocks examples
- 720 Minutes by Alexis André
- Archetype by Kjetil Golid
- Subscapes by Matt DesLauriers
- Box Light Studies by Zach Lieberman
- The Blocks of Art by Shvembldr
