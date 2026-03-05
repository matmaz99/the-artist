# Verlet Physics

## What it looks like
Realistic cloth, rope, or soft-body physics. Structures that sway, stretch, and bounce naturally.

## How it works  
Verlet integration: position updates without explicit velocity. Use distance constraints between points. Each frame: update positions, satisfy constraints iteratively, apply forces.

## Parameters
- **constraint stiffness**: how rigid connections are
- **iterations**: constraint solving passes
- **damping**: energy loss

## Minimal p5.js sketch
```javascript
class VerletPoint {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.oldPos = this.pos.copy();
    this.locked = false;
  }
  
  update() {
    if (this.locked) return;
    let vel = p5.Vector.sub(this.pos, this.oldPos);
    this.oldPos = this.pos.copy();
    this.pos.add(vel);
    this.pos.y += 0.5; // Gravity
  }
}

let points = [];
let restLength = 30;

function setup() {
  createCanvas(400, 400);
  for (let i = 0; i < 10; i++) {
    points.push(new VerletPoint(50 + i * restLength, 50));
  }
  points[0].locked = true;
}

function draw() {
  background(255);
  
  // Update
  for (let p of points) p.update();
  
  // Constrain
  for (let i = 0; i < points.length - 1; i++) {
    let p1 = points[i];
    let p2 = points[i + 1];
    let delta = p5.Vector.sub(p2.pos, p1.pos);
    let dist = delta.mag();
    let diff = (dist - restLength) / dist;
    delta.mult(0.5 * diff);
    
    if (!p1.locked) p1.pos.add(delta);
    if (!p2.locked) p2.pos.sub(delta);
  }
  
  // Draw
  stroke(0);
  for (let i = 0; i < points.length - 1; i++) {
    line(points[i].pos.x, points[i].pos.y, 
         points[i+1].pos.x, points[i+1].pos.y);
  }
  
  fill(255, 0, 0);
  for (let p of points) ellipse(p.pos.x, p.pos.y, 8);
}
```

## Combinations

**Typical role:** dynamics — simulates cloth, rope, and soft-body physics with constraints

**Works beautifully with:**
- **physics-simulation**: Verlet as the physics integration base — position-based dynamics
- **line-drawing**: Render Verlet structures as line segments — springs become drawn connections
- **particle-systems**: Verlet particles with distance constraints for connected systems
- **temporal-animation**: Physics naturally creates animation — constraints produce organic motion

**Creates tension with:**
- grid-layout: Verlet wants to deform; grids want to stay rigid. Use Verlet to simulate a flexible grid that sways.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like physical simulation → also look at physics-simulation for force-based dynamics
- If you want visual output → render Verlet mesh faces with stroke-hatching for a fabric look
- To invent something new → try Verlet cloth where each panel shows a different texture-synthesis pattern

## Art Blocks examples
- Memories of Qilin by Emily Xie
