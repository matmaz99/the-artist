# Framebuffer Feedback

## What it looks like
Recursive visual effects, trails that persist and transform, or echoing patterns. Previous frames influence current rendering.

## How it works  
Render to offscreen buffer (framebuffer). Each frame, draw previous buffer content (possibly transformed), then draw new content. Creates feedback loops and accumulation effects.

## Parameters
- **decay**: how fast old frames fade
- **transform**: scale, rotate, or translate previous frame
- **blend mode**: how old and new combine

## Minimal p5.js sketch
```javascript
let pg;

function setup() {
  createCanvas(400, 400);
  pg = createGraphics(width, height);
  pg.background(0);
}

function draw() {
  // Feedback: draw previous frame slightly scaled/faded
  pg.push();
  pg.translate(width/2, height/2);
  pg.scale(0.98);
  pg.translate(-width/2, -height/2);
  pg.tint(255, 250); // Slight fade
  pg.image(pg, 0, 0);
  pg.pop();
  
  // Draw new content
  pg.noStroke();
  pg.fill(255, 200, 100, 100);
  pg.ellipse(mouseX, mouseY, 30);
  
  image(pg, 0, 0);
}
```

## Combinations

**Typical role:** effect / accumulation — creates recursive trails and echoing patterns through frame re-reading

**Works beautifully with:**
- **particle-systems**: Feedback trails behind particles — each frame fades and accumulates
- **domain-warping**: Warp the feedback buffer for swirling, psychedelic trail patterns
- **blend-modes**: Control how new frame blends with accumulated buffer — multiply for darkening trails
- **temporal-animation**: Time-based feedback creates rhythmic pulse and breath in the accumulation

**Creates tension with:**
- posterize-quantization: Feedback wants smooth accumulation; posterize snaps it to bands. Can create interesting stepped-echo effects.
- texture-synthesis: Static texture and dynamic feedback compete — use texture very subtly or only at the final compositing stage.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like accumulation → also look at motion-trails for simpler persistent paths
- If you want more control → combine with blur-post-processing to soften the feedback
- To invent something new → try feedback where only certain color channels persist

## Art Blocks examples
- Calian by Eric De Giuli
- Ink by Iskra Velitchkova
- montreal friend scale by amon tobin
- RASTER by itsgalo
