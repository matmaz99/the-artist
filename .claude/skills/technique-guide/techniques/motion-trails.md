# Motion Trails

## What it looks like
Ghostly afterimages that trace movement. Objects leave fading trails showing their path through time.

## How it works  
Don't clear background completely each frame—draw semi-transparent rectangle over canvas. Objects drawn on top leave trails that gradually fade. Alpha controls trail length.

## Parameters
- **trail alpha**: transparency of fade overlay
- **trail length**: inverse of alpha (lower alpha = longer trails)

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(0);
}

function draw() {
  // Semi-transparent background creates trails
  fill(0, 20);
  rect(0, 0, width, height);
  
  // Draw moving object
  fill(255, 200, 100);
  noStroke();
  let x = width/2 + cos(frameCount * 0.05) * 150;
  let y = height/2 + sin(frameCount * 0.03) * 100;
  ellipse(x, y, 20);
}
```

## Combinations

**Typical role:** effect / time — creates persistent traces showing movement through space

**Works beautifully with:**
- **particle-systems**: Particle trails — the most common use. Each particle leaves a fading wake
- **temporal-animation**: Trail length and fade tied to animation speed for rhythmic traces
- **flow-fields**: Trails along flow lines visualize the invisible field directly
- **blend-modes**: Screen or additive trails glow; multiply trails darken like ink

**Creates tension with:**
- posterize-quantization: Trails want smooth fading; posterize wants steps. Creates interesting strobe-like banding in trails.
- texture-synthesis: Static texture and dynamic trails compete for visual attention. Use texture subtly under trails.

**Medium fit:** spray-paint

**Explore from here:**
- If you like persistence → also look at framebuffer-feedback for recursive accumulation
- If you want subtler traces → combine with ghost-stroke-doubling for lightweight echoes
- To invent something new → try trails where the trail itself warps with domain-warping over time

## Art Blocks examples
- Synapses by Chaosconstruct
