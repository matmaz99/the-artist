# Layered Composition

## What it looks like
Depth through overlapping elements. Foreground, midground, background create spatial hierarchy and visual richness.

## How it works  
Render multiple passes or layers, each with different content. Layers can have opacity, blend modes, or depth ordering. Can use framebuffers or z-index in DOM.

## Parameters
- **layer count**: number of depth planes
- **opacity**: transparency per layer
- **blend mode**: how layers combine
- **parallax**: depth-based motion offset

## Minimal p5.js sketch
```javascript
let layers = [];

function setup() {
  createCanvas(400, 400);
  
  // Create 3 layers
  for (let i = 0; i < 3; i++) {
    layers[i] = createGraphics(width, height);
  }
}

function draw() {
  background(240);
  
  // Layer 0: Background
  layers[0].clear();
  layers[0].noStroke();
  layers[0].fill(100, 150, 200);
  layers[0].ellipse(200, 200, 300);
  
  // Layer 1: Mid
  layers[1].clear();
  layers[1].fill(150, 200, 100);
  layers[1].ellipse(mouseX * 0.5, mouseY * 0.5, 150);
  
  // Layer 2: Foreground
  layers[2].clear();
  layers[2].fill(255, 150, 100);
  layers[2].ellipse(mouseX, mouseY, 60);
  
  // Composite
  for (let layer of layers) {
    image(layer, 0, 0);
  }
}
```

## Combinations

**Typical role:** structure — organizes visual elements into depth layers for spatial hierarchy

**Works beautifully with:**
- **blur-post-processing**: Blur distant layers for aerial perspective and depth of field
- **blend-modes**: Control how layers interact — multiply, screen, overlay for different moods
- **particle-systems**: Particles at different depths for parallax-like density
- **ghost-stroke-doubling**: Ghosts at different layers create atmospheric depth

**Creates tension with:**
- posterize-quantization: Posterize flattens the subtle transparency that makes layers work. Apply to individual layers before compositing.

**Medium fit:** gouache-layers, oil-impasto, watercolor-wash

**Explore from here:**
- If you like depth → also look at signed-distance-fields for distance-based depth
- If you want physical paint feel → each layer uses a different medium (wash, then gouache, then ink)
- To invent something new → try layers where each layer is a different time-slice of the same evolving system

## Art Blocks examples
- Apparitions by Aaron Penne
- Busiest by James Merrill
- Busy by James Merrill
- Fragments of an Infinite Field by Monica Rizzolli
- The Harvest by Per Kristian Stoveland
