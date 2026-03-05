# Differential Growth

## What it looks like
Organic forms that look grown rather than drawn—brain-like folds, coral, or intestinal patterns. Self-avoiding curves with controlled chaos.

## How it works  
Start with a curve or loop. Iteratively: split edges that are too long, push apart nodes that are too close, smooth the path. Balance growth with self-avoidance.

## Parameters
- **max edge length**: when to split
- **repulsion radius**: collision avoidance distance
- **repulsion force**: push strength
- **smoothing**: curve relaxation

## Minimal p5.js sketch
```javascript
class Node {
  constructor(x, y) {
    this.pos = createVector(x, y);
  }
}

let nodes = [];
let maxDist = 10;
let minDist = 7;

function setup() {
  createCanvas(400, 400);
  
  // Start with circle
  for (let a = 0; a < TWO_PI; a += 0.5) {
    nodes.push(new Node(200 + cos(a) * 50, 200 + sin(a) * 50));
  }
}

function draw() {
  background(255);
  
  // Split long edges
  for (let i = nodes.length - 1; i >= 0; i--) {
    let n1 = nodes[i];
    let n2 = nodes[(i + 1) % nodes.length];
    let d = p5.Vector.dist(n1.pos, n2.pos);
    
    if (d > maxDist) {
      let mid = p5.Vector.lerp(n1.pos, n2.pos, 0.5);
      nodes.splice(i + 1, 0, new Node(mid.x, mid.y));
    }
  }
  
  // Repulsion
  for (let i = 0; i < nodes.length; i++) {
    for (let j = 0; j < nodes.length; j++) {
      if (abs(i - j) < 2) continue;
      let d = p5.Vector.dist(nodes[i].pos, nodes[j].pos);
      if (d < minDist && d > 0) {
        let push = p5.Vector.sub(nodes[i].pos, nodes[j].pos);
        push.normalize();
        push.mult((minDist - d) * 0.05);
        nodes[i].pos.add(push);
      }
    }
  }
  
  // Draw
  noFill();
  stroke(0);
  beginShape();
  for (let n of nodes) vertex(n.pos.x, n.pos.y);
  endShape(CLOSE);
  
  fill(0);
  for (let n of nodes) ellipse(n.pos.x, n.pos.y, 3);
}
```

## Combinations

**Typical role:** generator — creates organic forms that look grown rather than drawn

**Works beautifully with:**
- **curve-smoothing**: Smooth differential growth curves into flowing organic surfaces
- **verlet-physics**: Physics-based growth with real collision and tension constraints
- **flow-fields**: Growth direction biased by flow field — organisms that grow with the current
- **noise-density-scatter**: Scatter growth seeds in organic clusters for natural-looking starting points

**Creates tension with:**
- grid-layout: Growth is inherently anti-grid. Interesting if growth starts from grid points then breaks free.
- symmetry-mirroring: Natural growth is asymmetric. Forced symmetry looks unnatural — use bilateral symmetry at most.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like organic forms → also look at reaction-diffusion, l-systems
- If you want to fill the growth with texture → use stroke-hatching inside grown regions
- To invent something new → try differential growth on the boundary of a voronoi-tessellation

## Art Blocks examples
- Spaghetti Bones by Joshua Bagley
