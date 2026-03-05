# Procedural Textures

## What it looks like
Surface patterns like paper grain, canvas texture, or organic materials. Adds tactile quality to flat digital images.

## How it works  
Layer noise patterns, scanlines, or micro-geometry. Can use photo textures, procedural noise, or particle scattering. Blend modes control how texture interacts with base colors.

## Parameters
- **scale**: texture detail level
- **opacity**: visibility of texture
- **blend mode**: multiply, overlay, etc.

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  background(220);
  
  // Base shapes
  fill(255, 100, 100);
  rect(50, 50, 300, 300);
  
  // Add paper texture
  loadPixels();
  for (let i = 0; i < pixels.length; i += 4) {
    let grain = random(-20, 20);
    pixels[i] += grain;
    pixels[i + 1] += grain;
    pixels[i + 2] += grain;
  }
  updatePixels();
  
  // Scanlines
  stroke(0, 30);
  for (let y = 0; y < height; y += 2) {
    line(0, y, width, y);
  }
}
```

## Combinations

**Typical role:** surface — adds material quality (paper grain, canvas weave, rough surface) to the artwork

**Works beautifully with:**
- **blend-modes**: Texture as overlay blend onto base imagery — subtle surface presence
- **line-drawing**: Textured strokes — the paper grain shows through drawn marks
- **deckled-edge**: Paper texture extends to the ragged borders for cohesive material feel
- **stroke-hatching**: Hatching on textured paper — graphite catches the grain differently

**Creates tension with:**
- blur-post-processing: Blur destroys texture detail — apply texture after blur, or selectively protect textured areas.
- alpha-spatter: Both add surface noise — using both risks visual clutter. One for macro texture, one for micro.

**Medium fit:** fine-pencil, gouache-layers, spray-paint, etching-printmaking, oil-impasto, charcoal-conte

**Explore from here:**
- If you like surface quality → also look at deckled-edge for border-specific texture
- If you want specific materials → try different noise patterns (Worley for stone, Perlin for canvas, grid for weave)
- To invent something new → try texture that responds to paint thickness — thick areas have ridge texture, thin areas show paper

## Art Blocks examples
- Bent by ippsketch
- Fontana by Harvey Rayner | patterndotco
- Memories of Digital Data by Kazuhiro Tanimoto
- Memories of Qilin by Emily Xie
- Para Bellum by Matty Mariansky
