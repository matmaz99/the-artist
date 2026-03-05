# Blend Mode Layering

## What it looks like
Unexpected color interactions—layers that multiply, screen, overlay, or add. Creates luminous, painterly, or glitchy effects.

## How it works  
Instead of simple alpha compositing, use math operations on pixel values. Multiply darkens, screen lightens, overlay combines both. Requires canvas blendMode() or shader blending.

## Parameters
- **blend mode**: multiply, screen, overlay, add, etc.
- **layer opacity**: strength of effect

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  background(255);
  
  blendMode(MULTIPLY);
  fill(255, 0, 0, 200);
  ellipse(150, 200, 200);
  
  fill(0, 0, 255, 200);
  ellipse(250, 200, 200);
  
  // Overlapping area becomes darker (red * blue)
  
  blendMode(SCREEN);
  fill(255, 255, 0, 200);
  ellipse(200, 250, 150);
  
  // Overlapping with yellow becomes lighter
}
```

## Combinations

**Typical role:** compositing — controls how visual layers interact optically

**Works beautifully with:**
- **layered-composition**: Blend modes are the language of layer interaction — multiply, screen, overlay
- **texture-synthesis**: Blend textures onto base — overlay for subtle, multiply for dramatic
- **alpha-spatter**: Spatter through blend modes creates depth — screen for glow, multiply for ink
- **ghost-stroke-doubling**: Multiply or screen blending between ghost and primary creates atmospheric depth

**Creates tension with:**
- posterize-quantization: Blend modes create smooth transitions; posterize flattens them. Apply posterize after blending, not during.

**Medium fit:** gouache-layers, watercolor-wash, oil-impasto

**Explore from here:**
- If you like layer interactions → also look at layered-composition, framebuffer-feedback
- If you want physical paint feel → multiply mode simulates transparent glazing like watercolor
- To invent something new → try custom blend functions that simulate specific pigment chemistry

## Art Blocks examples
- Elementals by Michael Connolly
- Torrent by Jeres
- Para Bellum by Matty Mariansky
