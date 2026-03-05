# SVG Generation

## What it looks like
Crisp, resolution-independent vector graphics. Lines and shapes that scale infinitely without pixelation.

## How it works  
Build XML strings or DOM elements defining SVG paths, circles, polygons. Use path commands (M = move, L = line, C = curve). Export or render inline in HTML.

## Parameters
- **viewBox**: coordinate system bounds
- **path commands**: drawing instructions
- **fill/stroke**: styling properties

## Minimal p5.js sketch
```javascript
function setup() {
  noCanvas();
  let svg = createSVG(400, 400);
  
  for (let i = 0; i < 10; i++) {
    let x = random(50, 350);
    let y = random(50, 350);
    let r = random(10, 40);
    let circle = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
    circle.setAttribute('cx', x);
    circle.setAttribute('cy', y);
    circle.setAttribute('r', r);
    circle.setAttribute('fill', `rgb(${random(255)}, ${random(255)}, ${random(255)})`);
    svg.appendChild(circle);
  }
  
  document.body.appendChild(svg);
}

function createSVG(w, h) {
  let svg = document.createElementNS('http://www.w3.org/2000/svg', 'svg');
  svg.setAttribute('width', w);
  svg.setAttribute('height', h);
  svg.setAttribute('viewBox', `0 0 ${w} ${h}`);
  return svg;
}
```

## Combinations

**Typical role:** output — produces resolution-independent vector graphics for print and plot

**Works beautifully with:**
- **grid-layout**: SVG for clean, crisp vector grids — scales perfectly at any resolution
- **bezier-curves**: SVG path curves — the native curve format for vector graphics
- **line-drawing**: All line-based art translates perfectly to SVG paths
- **polygon-operations**: Boolean operations on SVG paths for complex vector shapes

**Creates tension with:**
- alpha-spatter: Thousands of spray dots are expensive as individual SVG elements. Use raster for spatter, SVG for lines.
- blur-post-processing: SVG blur filters are computationally expensive — prefer raster for heavy blur effects.

**Medium fit:** fine-pencil, ink-on-paper, etching-printmaking

**Explore from here:**
- If you like vector output → also look at line-drawing for pen-plotter-ready art
- If you want physical output → SVG is ideal for pen plotters and laser cutters
- To invent something new → try SVG with animated SMIL paths for evolving vector art

## Art Blocks examples
- Act of Emotion by Kelly Milligan
- Aerial View by daLenz
- Algobots by Stina Jones
- Asemica by Emily Edelman, Dima Ofman, Andrew Badr
- Unigrids by Zeblocks
