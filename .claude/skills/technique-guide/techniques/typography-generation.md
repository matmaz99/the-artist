# Generative Typography

## What it looks like
Text as visual element—letterforms that morph, custom glyphs, or typographic compositions. Text becomes shape and pattern.

## How it works  
Use font metrics to place glyphs, or define custom letterforms as paths. Can distort existing fonts or generate from scratch using geometric rules. SVG paths or canvas text() with transforms.

## Parameters
- **font/glyph data**: letterform definitions
- **spacing**: kerning and leading
- **transforms**: rotation, scale, skew per character

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  textSize(64);
  textAlign(CENTER, CENTER);
}

function draw() {
  background(255);
  
  push();
  translate(width/2, height/2);
  
  let chars = 'GENERATIVE';
  let angleStep = TWO_PI / chars.length;
  
  for (let i = 0; i < chars.length; i++) {
    push();
    rotate(angleStep * i);
    translate(0, -120);
    rotate(frameCount * 0.01);
    
    fill(0);
    text(chars[i], 0, 0);
    pop();
  }
  
  pop();
}
```

## Combinations

**Typical role:** form / content — uses letterforms as visual elements in the composition

**Works beautifully with:**
- **grid-layout**: Typographic grids for structured text layouts — the foundation of type design
- **hash-randomness**: Unique letterforms per token — generative typography from seeds
- **signed-distance-fields**: SDF-based text rendering for smooth, scalable letterforms
- **color-palettes**: Color letterforms as visual elements, not just text

**Creates tension with:**
- flow-fields: Text wants readability; flow wants distortion. Use flow for decorative type that doesn't need to be read.
- erode-dilate: Erosion can destroy letterform readability — use only for intentionally degraded/aged type.

**Medium fit:** etching-printmaking

**Explore from here:**
- If you like text as art → also look at line-drawing for custom glyph construction
- If you want more organic type → combine with differential-growth for type that grows and evolves
- To invent something new → try letterforms whose strokes are flow-field traces

## Art Blocks examples
- 27-Bit Digital by kai
- Asemica by Emily Edelman, Dima Ofman, Andrew Badr
- Dopamine Machines by Steve Pikelny
- Para Bellum by Matty Mariansky
- The Blocks of Art by Shvembldr
