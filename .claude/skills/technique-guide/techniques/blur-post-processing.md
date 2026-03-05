# Blur & Post-Processing

## What it looks like
Soft, dreamy visuals with defocused edges and glowing highlights. Bokeh effects, motion blur, or atmospheric depth.

## How it works  
Multi-pass rendering: render scene to framebuffer, then apply blur shader(s) sampling neighboring pixels. Gaussian blur uses weighted samples in two passes (horizontal then vertical) for efficiency.

## Parameters
- **blur radius**: spread of blur effect
- **passes**: number of blur iterations
- **kernel size**: sample neighborhood
- **bloom threshold**: which values glow

## Minimal p5.js sketch
```javascript
let pg;

function setup() {
  createCanvas(400, 400);
  pg = createGraphics(width, height);
}

function draw() {
  // Draw to buffer
  pg.background(255);
  pg.fill(255, 200, 0);
  pg.noStroke();
  pg.ellipse(mouseX, mouseY, 60);
  
  // Simple box blur
  loadPixels();
  pg.loadPixels();
  
  for (let x = 2; x < width-2; x++) {
    for (let y = 2; y < height-2; y++) {
      let idx = (x + y * width) * 4;
      // Average surrounding pixels (simplified)
      let sum = 0;
      for (let dx = -2; dx <= 2; dx++) {
        for (let dy = -2; dy <= 2; dy++) {
          let nidx = ((x+dx) + (y+dy) * width) * 4;
          sum += pg.pixels[nidx];
        }
      }
      pixels[idx] = sum / 25;
      pixels[idx+1] = pixels[idx];
      pixels[idx+2] = pixels[idx];
      pixels[idx+3] = 255;
    }
  }
  updatePixels();
}
```

## Combinations

**Typical role:** post-process — softens, glows, or defocuses the rendered image

**Works beautifully with:**
- **particle-systems**: Blur trails behind particles for motion feel and atmospheric glow
- **lighting-shading**: Bloom on bright areas creates cinematic glow and depth of field
- **layered-composition**: Blur distant layers for aerial perspective — sharp foreground, soft background
- **gradient-systems**: Smooth any banding artifacts in gradients for seamless transitions

**Creates tension with:**
- stroke-hatching: Blur destroys the fine detail that makes hatching interesting. If using both, blur selectively — background only.
- texture-synthesis: Blur fights texture detail. Apply blur before texture, not after.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like the soft look → also look at ghost-stroke-doubling for a hand-drawn softness
- If you want selective focus → combine with signed-distance-fields to mask blur by depth
- To invent something new → try directional blur that follows flow-fields instead of uniform blur

## Art Blocks examples
- Ceramics by Charlotte Dann
- JIOMETORY [no compute] by samsy
- NimBuds by Bryan Brinkman
- phase by Loren Bednar
- Solar Transits by Robert Hodgin
