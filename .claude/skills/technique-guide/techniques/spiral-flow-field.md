# Spiral Flow Field

## What it looks like
Swirling vortex patterns where particles orbit around one or more centers, creating hurricane-like spirals, whirlpools, or galaxy arms. The flow has a rotational energy that standard noise fields lack.

## How it works
A standard Perlin noise flow field is augmented with a vortex term. For each point, compute the angle to a center point and add an angular offset proportional to the square root of the distance. This creates an Archimedean spiral tendency. The spiral strength is blended with the noise field so particles spiral inward or outward while still following organic noise curves.

## Parameters
- **spiral strength**: how much rotational offset to add
- **center x/y**: vortex origin point
- **falloff**: how spiral influence changes with distance (sqrt, linear, log)
- **noise blend**: ratio of spiral angle to noise angle

## Minimal p5.js sketch
```javascript
let particles = [];

function setup() {
  createCanvas(400, 400);
  background(245);
  for (let i = 0; i < 200; i++) {
    particles.push(createVector(random(width), random(height)));
  }
}

function draw() {
  let cx = width / 2, cy = height / 2;
  for (let p of particles) {
    let dx = p.x - cx, dy = p.y - cy;
    let d = sqrt(dx * dx + dy * dy);
    let spiralAngle = atan2(dy, dx) + sqrt(d) * 0.15;
    let noiseAngle = noise(p.x * 0.008, p.y * 0.008) * TWO_PI * 2;
    let angle = lerp(spiralAngle, noiseAngle, 0.4);

    p.x += cos(angle) * 1.2;
    p.y += sin(angle) * 1.2;

    if (p.x < 0 || p.x > width || p.y < 0 || p.y > height) {
      p.set(random(width), random(height));
    }
    stroke(0, 8);
    point(p.x, p.y);
  }
}
```

## Combinations

**Typical role:** structure / motion — creates swirling vortex patterns with orbital movement

**Works beautifully with:**
- **flow-fields**: Spiral modulation layered on top of noise fields for complex turbulence
- **perlin-simplex-noise**: Noise provides the organic base that spiral distorts into vortices
- **particle-systems**: Particles trace spiral trajectories — the visual output of the field
- **fat-line-stroke**: Thick ribbons spiraling create dramatic, dynamic compositions

**Creates tension with:**
- grid-layout: Spirals are radial; grids are rectilinear. Interesting if spiral warps a grid into circular form.
- symmetry-mirroring: Multiple spiral centers can create their own symmetric arrangement without forced mirror symmetry.

**Medium fit:** watercolor-wash, oil-impasto

**Explore from here:**
- If you like rotational movement → also look at flow-fields for more general directional flow
- If you want tighter control → use signed-distance-fields to define spiral paths mathematically
- To invent something new → try spiral fields where the rotation speed varies with fbm-noise

## Art Blocks examples
- Fidenza by Tyler Hobbs
- Anticyclone by William Mapan
- Vortex by Jen Stark
