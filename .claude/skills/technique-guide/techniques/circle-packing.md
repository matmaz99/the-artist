# Circle Packing

## What it looks like
Organic arrangements of circles filling space without overlap. Like bubbles or cells, creating natural-looking patterns.

## How it works  
Place circles one at a time, checking distance to existing circles. Only add if no overlap. Can grow circles iteratively or use more advanced algorithms like Poisson disk sampling.

## Parameters
- **min/max radius**: circle size range
- **attempts**: placement tries before giving up
- **padding**: minimum gap between circles

## Minimal p5.js sketch
```javascript
let circles = [];

function setup() {
  createCanvas(400, 400);
  
  for (let i = 0; i < 1000; i++) {
    let x = random(width);
    let y = random(height);
    let r = random(5, 40);
    
    let valid = true;
    for (let c of circles) {
      let d = dist(x, y, c.x, c.y);
      if (d < r + c.r) {
        valid = false;
        break;
      }
    }
    
    if (valid) {
      circles.push({x, y, r});
    }
  }
  
  noLoop();
}

function draw() {
  background(255);
  noFill();
  stroke(0);
  for (let c of circles) {
    ellipse(c.x, c.y, c.r * 2);
  }
}
```

## Combinations

**Typical role:** layout — fills space with non-overlapping circles for organic composition

**Works beautifully with:**
- **color-palettes**: Color circles by size, position, or random palette sampling
- **voronoi-tessellation**: Voronoi cells around circle centers — dual representation of same layout
- **concentric-ring-fill**: Fill packed circles with concentric rings for target/tree-ring pattern
- **noise-density-scatter**: Pack more circles where noise is dense, fewer where sparse — organic clustering

**Creates tension with:**
- grid-layout: Grid wants regularity; packing wants organic. Use grid as initial seed positions then relax into packing.

**Medium fit:** ceramic-glaze

**Explore from here:**
- If you like space-filling → also look at voronoi-tessellation, recursive-subdivision
- If you want more variation → fill each circle with a different technique (hatching, gradient, spatter)
- To invent something new → try circle packing where circles grow over time with differential-growth

## Art Blocks examples
- Pre-Process by Casey REAS
- Ringers by Dmitri Cherniak
- Singularity by Hideki Tsukamoto
