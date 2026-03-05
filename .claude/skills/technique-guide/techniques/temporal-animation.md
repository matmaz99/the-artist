# Temporal Animation

## What it looks like
Motion over time—shapes that drift, pulse, rotate, or morph. The artwork evolves continuously or cycles through states.

## How it works  
Variables change each frame based on time, trigonometric functions, or animation curves. Common patterns: linear interpolation, easing functions, sine waves, or frame counters that trigger state changes.

## Parameters
- **speed**: how fast changes occur
- **easing**: acceleration curves
- **loop duration**: cycle length
- **phase**: offset in animation cycle

## Minimal p5.js sketch
```javascript
let angle = 0;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(255, 10); // Trail effect
  translate(width/2, height/2);
  
  let x = cos(angle) * 100;
  let y = sin(angle) * 100;
  
  fill(100, 150, 255);
  noStroke();
  ellipse(x, y, 30);
  
  angle += 0.05; // Animation speed
}
```

## Combinations

**Typical role:** time — adds motion, evolution, and change over time to static compositions

**Works beautifully with:**
- **particle-systems**: Animate particle motion — the most common animation subject
- **webgl-shaders**: Time uniform drives shader animation for smooth, GPU-accelerated motion
- **reaction-diffusion**: Animate simulation evolution for mesmerizing growth patterns
- **flow-fields**: Animate field evolution over time for shifting currents

**Creates tension with:**
- svg-generation: SVG is primarily static — animation requires SMIL or CSS which adds complexity.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like motion → also look at physics-simulation for physically realistic animation
- If you want subtle change → very slow parameter drift creates the Ambiant living-painting effect
- To invent something new → try animation where time flows at different speeds in different regions (via fbm-noise)

## Art Blocks examples
- Dopamine Machines by Steve Pikelny
- Endless Nameless by Rafaël Rozendaal
- entretiempos by Marcelo Soria-Rodríguez
- Frammenti by Stefano Contiero
- Human Unreadable by operator
