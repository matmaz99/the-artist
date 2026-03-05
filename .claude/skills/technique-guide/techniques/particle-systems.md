# Particle Systems

## What it looks like
Swarms, clouds, or trails of tiny elements that move, interact, and create emergent patterns. Can simulate stars, fireflies, crowds, or abstract entities.

## How it works  
Arrays of objects store particle positions and velocities. Each frame, update positions based on physics (forces, acceleration) and draw each particle. Can add behaviors like attraction, repulsion, or randomness.

## Parameters
- **particle count**: number of entities
- **forces**: gravity, drag, noise
- **lifespan**: when particles die/respawn
- **trail length**: motion blur effect

## Minimal p5.js sketch
```javascript
let particles = [];

function setup() {
  createCanvas(400, 400);
  for (let i = 0; i < 50; i++) {
    particles.push({
      x: width/2,
      y: height/2,
      vx: random(-2, 2),
      vy: random(-2, 2)
    });
  }
}

function draw() {
  background(255, 20);
  
  for (let p of particles) {
    p.x += p.vx;
    p.y += p.vy;
    
    if (p.x < 0 || p.x > width) p.vx *= -1;
    if (p.y < 0 || p.y > height) p.vy *= -1;
    
    fill(0, 100, 255, 200);
    noStroke();
    ellipse(p.x, p.y, 8);
  }
}
```

## Combinations

**Typical role:** dynamics — creates swarms and trails of moving elements with emergent behavior

**Works beautifully with:**
- **flow-fields**: Particles follow field vectors — the fundamental flow visualization
- **physics-simulation**: Add attraction, repulsion, gravity for realistic particle motion
- **alpha-spatter**: Particles become spray dots with noise-driven opacity
- **motion-trails**: Each particle leaves a fading wake for persistent visualization

**Creates tension with:**
- grid-layout: Particles want to move freely; grids constrain. Interesting if particles are born on grid points then released.
- posterize-quantization: Particles are continuous; posterize is discrete. Quantize particle trails for a printmaking look.

**Medium fit:** spray-paint

**Explore from here:**
- If you like moving elements → also look at verlet-physics for constrained dynamics
- If you want static results → render particle positions as a final still image, not animation
- To invent something new → try particles that leave different mark types depending on their speed (fast=spatter, slow=stroke)

## Art Blocks examples
- 720 Minutes by Alexis André
- Scribbled Boundaries by William Tan
- Bokeh by mpkoz
- Cerebellum by Laya Mathikshara & Santiago
- Chimera by mpkoz
