# Physics Simulation

## What it looks like
Natural motion—objects that bounce, swing, orbit, or attract each other. Movement follows physical laws rather than arbitrary paths.

## How it works  
Implement Newton's laws: F = ma. Calculate forces (gravity, springs, drag), update velocities, update positions. Detect and resolve collisions. Can use simplified physics or full-fledged engines.

## Parameters
- **forces**: gravity, attraction, repulsion
- **mass**: object weight affects motion
- **damping**: friction/air resistance
- **timestep**: simulation precision

## Minimal p5.js sketch
```javascript
let ball = {x: 200, y: 50, vx: 2, vy: 0};
let gravity = 0.3;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(255);
  
  // Apply forces
  ball.vy += gravity;
  ball.x += ball.vx;
  ball.y += ball.vy;
  
  // Bounce
  if (ball.y > height - 20) {
    ball.y = height - 20;
    ball.vy *= -0.8; // Energy loss
  }
  if (ball.x < 20 || ball.x > width - 20) {
    ball.vx *= -1;
  }
  
  fill(100, 150, 255);
  ellipse(ball.x, ball.y, 40);
}
```

## Combinations

**Typical role:** dynamics — adds realistic forces (gravity, attraction, collision) to elements

**Works beautifully with:**
- **particle-systems**: Physics-based particle motion — the most natural combination
- **verlet-physics**: Constraint-based simulation for cloth, rope, soft bodies
- **flow-fields**: Physics forces modulate flow field strength — turbulence from collision
- **temporal-animation**: Physics inherently creates animation — forces produce motion over time

**Creates tension with:**
- grid-layout: Physics wants natural motion; grids want structure. Use grid as collision boundaries.
- symmetry-mirroring: Physics is inherently asymmetric — mirrored physics looks unnatural.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like natural motion → also look at verlet-physics for constraint-based dynamics
- If you want frozen physics → simulate then render the final state as a still image
- To invent something new → try physics where gravity direction changes with domain-warping

## Art Blocks examples
- Ancient Courses of Fictional Rivers by Robert Hodgin
- Dipolar by Junia Farquhar
- Edifice by Ben Kovach
- Pre-Process by Casey REAS
- Singularity by Hideki Tsukamoto
