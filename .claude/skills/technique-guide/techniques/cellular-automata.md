# Cellular Automata

## What it looks like
Emergent patterns from simple rules—oscillators, gliders, or chaotic complexity. Like Conway's Game of Life.

## How it works  
Grid of cells with states (on/off or multiple states). Each generation, cells update based on neighbor states following fixed rules. Simple local rules create global patterns.

## Parameters
- **rule set**: birth/survival conditions
- **initial state**: starting pattern
- **neighborhood**: Moore (8) or von Neumann (4)

## Minimal p5.js sketch
```javascript
let grid, cols, rows;
let resolution = 10;

function setup() {
  createCanvas(400, 400);
  cols = width / resolution;
  rows = height / resolution;
  
  grid = make2DArray(cols, rows);
  for (let i = 0; i < cols; i++) {
    for (let j = 0; j < rows; j++) {
      grid[i][j] = floor(random(2));
    }
  }
}

function draw() {
  background(255);
  
  // Draw
  for (let i = 0; i < cols; i++) {
    for (let j = 0; j < rows; j++) {
      let x = i * resolution;
      let y = j * resolution;
      fill(grid[i][j] ? 0 : 255);
      stroke(200);
      rect(x, y, resolution, resolution);
    }
  }
  
  // Compute next generation
  let next = make2DArray(cols, rows);
  for (let i = 0; i < cols; i++) {
    for (let j = 0; j < rows; j++) {
      let neighbors = countNeighbors(grid, i, j);
      
      // Conway's Game of Life rules
      if (grid[i][j] === 1 && (neighbors < 2 || neighbors > 3)) {
        next[i][j] = 0;
      } else if (grid[i][j] === 0 && neighbors === 3) {
        next[i][j] = 1;
      } else {
        next[i][j] = grid[i][j];
      }
    }
  }
  
  grid = next;
}

function countNeighbors(grid, x, y) {
  let sum = 0;
  for (let i = -1; i <= 1; i++) {
    for (let j = -1; j <= 1; j++) {
      let col = (x + i + cols) % cols;
      let row = (y + j + rows) % rows;
      sum += grid[col][row];
    }
  }
  sum -= grid[x][y];
  return sum;
}

function make2DArray(cols, rows) {
  let arr = new Array(cols);
  for (let i = 0; i < cols; i++) {
    arr[i] = new Array(rows);
  }
  return arr;
}
```

## Combinations

**Typical role:** generator — creates emergent patterns from simple local rules

**Works beautifully with:**
- **grid-layout**: CA runs naturally on structured grids — the grid is its native habitat
- **color-palettes**: Map cell states to curated colors — state 0 = background, states 1-3 = palette
- **posterize-quantization**: CA states are already quantized — posterize reinforces the discrete look
- **temporal-animation**: Animate CA generations over time for mesmerizing evolution

**Creates tension with:**
- flow-fields: CA wants discrete grid steps; flow wants continuous curves. Interesting hybrid if CA influences flow field angles.
- curve-smoothing: CA outputs are inherently jagged — smoothing fights the aesthetic. Embrace the pixels or don't use CA.

**Medium fit:** woven-textile

**Explore from here:**
- If you like emergent patterns → also look at reaction-diffusion, l-systems
- If you want smoother forms → use marching-squares to extract contours from CA states
- To invent something new → try CA rules where cell state determines which mark type is drawn

## Art Blocks examples
- Screens by Thomas Lin Pedersen
