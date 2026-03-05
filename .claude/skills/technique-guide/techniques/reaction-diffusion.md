# Reaction-Diffusion

## What it looks like
Organic, coral-like patterns with spots and stripes. Resembles animal markings, chemical reactions, or biological growth.

## How it works  
Two chemicals diffuse and react in a grid. Gray-Scott equations model activator-inhibitor dynamics. Each cell updates based on neighbors and reaction rates. Creates stable patterns.

## Parameters
- **feed rate**: nutrient addition
- **kill rate**: chemical removal
- **diffusion rates**: spread of chemicals A and B

## Minimal p5.js sketch
```javascript
// Simplified Gray-Scott reaction-diffusion
let grid, next;
let dA = 1.0, dB = 0.5;
let feed = 0.055, kill = 0.062;

function setup() {
  createCanvas(400, 400);
  grid = create2DArray(width, height);
  next = create2DArray(width, height);
  
  // Initialize
  for (let x = 0; x < width; x++) {
    for (let y = 0; y < height; y++) {
      grid[x][y] = {a: 1, b: 0};
      if (x > width/2 - 20 && x < width/2 + 20 && 
          y > height/2 - 20 && y < height/2 + 20) {
        grid[x][y].b = 1;
      }
    }
  }
}

function draw() {
  for (let x = 1; x < width - 1; x++) {
    for (let y = 1; y < height - 1; y++) {
      let a = grid[x][y].a;
      let b = grid[x][y].b;
      
      // Laplacian (simplified)
      let laplaceA = 0, laplaceB = 0;
      laplaceA = -a + (grid[x-1][y].a + grid[x+1][y].a + grid[x][y-1].a + grid[x][y+1].a) / 4;
      laplaceB = -b + (grid[x-1][y].b + grid[x+1][y].b + grid[x][y-1].b + grid[x][y+1].b) / 4;
      
      // Reaction
      next[x][y].a = a + (dA * laplaceA - a * b * b + feed * (1 - a));
      next[x][y].b = b + (dB * laplaceB + a * b * b - (kill + feed) * b);
      
      next[x][y].a = constrain(next[x][y].a, 0, 1);
      next[x][y].b = constrain(next[x][y].b, 0, 1);
    }
  }
  
  [grid, next] = [next, grid];
  
  // Draw
  loadPixels();
  for (let x = 0; x < width; x++) {
    for (let y = 0; y < height; y++) {
      let val = (grid[x][y].a - grid[x][y].b) * 255;
      let idx = (x + y * width) * 4;
      pixels[idx] = val;
      pixels[idx + 1] = val;
      pixels[idx + 2] = val;
      pixels[idx + 3] = 255;
    }
  }
  updatePixels();
}

function create2DArray(w, h) {
  let arr = new Array(w);
  for (let i = 0; i < w; i++) {
    arr[i] = new Array(h);
    for (let j = 0; j < h; j++) {
      arr[i][j] = {a: 0, b: 0};
    }
  }
  return arr;
}
```

## Combinations

**Typical role:** generator — creates organic spot/stripe patterns through chemical simulation

**Works beautifully with:**
- **domain-warping**: Distort reaction patterns for swirling, organic growth forms
- **color-palettes**: Map reaction concentrations to curated colors — high = one hue, low = another
- **temporal-animation**: Animate the simulation over time for mesmerizing pattern evolution
- **texture-synthesis**: Reaction patterns as surface texture on other forms

**Creates tension with:**
- grid-layout: Reaction-diffusion is inherently organic — grids constrain it. Interesting as containment.
- posterize-quantization: Reaction already creates sharp boundaries between spots and background — posterize may be redundant.

**Medium fit:** ceramic-glaze

**Explore from here:**
- If you like emergent patterns → also look at cellular-automata, differential-growth
- If you want more control → vary feed/kill rates across the canvas with fbm-noise for regional pattern types
- To invent something new → try reaction-diffusion on a voronoi-tessellation mesh instead of a regular grid

## Art Blocks examples
- Calian by Eric De Giuli
