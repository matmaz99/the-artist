# Flow Fields

## What it looks like
Graceful, curving paths that flow like wind or water. Particles follow invisible force vectors, creating organic swirls, eddies, and streams across the canvas.

## How it works  
A grid of angle values (often from Perlin noise) defines a vector field. Particles read the angle at their position and move in that direction. Over many steps, they trace smooth curves through the field.

## Parameters
- **field resolution**: grid density
- **noise scale**: smoothness of field
- **particle count**: number of traces
- **step size**: path resolution

## Minimal p5.js sketch
```javascript
let particles = [];

function setup() {
  createCanvas(400, 400);
  background(255);
  for (let i = 0; i < 100; i++) {
    particles.push(createVector(random(width), random(height)));
  }
}

function draw() {
  for (let p of particles) {
    let angle = noise(p.x * 0.01, p.y * 0.01) * TWO_PI * 2;
    p.x += cos(angle);
    p.y += sin(angle);
    
    if (p.x < 0 || p.x > width || p.y < 0 || p.y > height) {
      p.set(random(width), random(height));
    }
    
    stroke(0, 10);
    point(p.x, p.y);
  }
}
```

## Combinations

**Typical role:** structure / motion — defines how elements move through space along invisible currents

**Works beautifully with:**
- **perlin-simplex-noise**: Generates the underlying vector field — noise angle at each point
- **particle-systems**: Particles follow the field — the most classic flow field visualization
- **fat-line-stroke**: Thick ribbons along flow create Fidenza-like compositions
- **stroke-hatching**: Hatch lines that follow flow direction for cross-contour shading

**Creates tension with:**
- grid-layout: Grid wants structure; flow wants freedom. Flow within grid cells can be powerful — contained currents.
- symmetry-mirroring: Flow is inherently asymmetric — mirrored flow looks artificial unless the field itself is symmetric.

**Medium fit:** watercolor-wash, charcoal-conte, oil-impasto

**Explore from here:**
- If you like directional movement → also look at spiral-flow-field for vortex patterns
- If you want visible paths → combine with motion-trails for persistent trajectories
- To invent something new → try flow fields derived from image gradients or signed-distance-fields

## Art Blocks examples
- Alan Ki Aankhen by Fahad Karim
- Scribbled Boundaries by William Tan
- Ancient Courses of Fictional Rivers by Robert Hodgin
- Anticyclone by William Mapan
- Dipolar by Junia Farquhar
