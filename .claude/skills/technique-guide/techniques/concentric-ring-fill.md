# Concentric Ring Fill

## What it looks like
Circles filled with alternating colored rings, creating a target or tree-ring pattern. Each ring pair has a consistent rhythm, and the effect across many circles reads like a field of bullseyes or cross-sections of wood.

## How it works
For each circle, draw progressively smaller concentric rings from the outer radius inward. Alternate between two colors at a fixed ring width. The fill is purely geometric: a series of arc or ellipse calls with decreasing radii. Varying the ring width, number of rings, or color pair per circle adds variety across a composition.

## Parameters
- **outer radius**: size of the circle
- **ring width**: thickness of each band
- **color A / color B**: the two alternating fill colors
- **ring count**: how many bands fit inside the radius

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(245);
  noStroke();

  let colors = [
    ['#1a1a2e', '#e0d8c0'],
    ['#c44536', '#e0d8c0'],
    ['#2d6a4f', '#e0d8c0']
  ];

  for (let i = 0; i < 12; i++) {
    let x = random(50, 350);
    let y = random(50, 350);
    let r = random(25, 60);
    let ringW = random(3, 8);
    let pair = random(colors);

    for (let rad = r; rad > 0; rad -= ringW) {
      fill(rad % (ringW * 2) < ringW ? pair[0] : pair[1]);
      ellipse(x, y, rad * 2);
    }
  }
}
```

## Combinations

**Typical role:** fill / motif — fills circular areas with repeating ring patterns

**Works beautifully with:**
- **circle-packing**: Fill packed circles with concentric rings for a dense decorative field
- **grid-layout**: Place ringed circles on a structured grid for tile-like regularity
- **symmetry-mirroring**: Radial symmetry of rings amplifies pattern regularity — mandala-like
- **cosine-gradient-palette**: Color rings with smooth gradient transitions across the ring sequence

**Creates tension with:**
- flow-fields: Rings are static and centered; flow is directional. Interesting if flow deforms the rings into ovals.
- alpha-spatter: Spatter disrupts the clean ring structure — use very lightly for aged/weathered look.

**Medium fit:** woven-textile, ceramic-glaze

**Explore from here:**
- If you like repeating circular motifs → also look at seigaiha-wave-pattern, truchet-tiles
- If you want more organic feel → add noise-density-scatter to vary ring spacing
- To invent something new → try concentric rings that are actually spiral-flow-field trajectories

## Art Blocks examples
- Ringers by Dmitri Cherniak
- Dot Matrix by Ben Kovach
- Gazers by Matt Kane
