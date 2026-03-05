# Domain Warping

## What it looks like
Distorted, swirling patterns where shapes seem pulled by invisible forces. Noise that would be smooth becomes twisted into organic, psychedelic forms.

## How it works  
Instead of directly sampling noise at (x, y), first distort the coordinates themselves using noise: nx = x + noise(x, y) * strength. This creates feedback loops and intricate, non-repeating patterns.

## Parameters
- **warp strength**: intensity of distortion
- **warp layers**: multiple distortion passes
- **warp scale**: frequency of distortion noise

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  loadPixels();
  for (let x = 0; x < width; x++) {
    for (let y = 0; y < height; y++) {
      // Domain warp: distort coordinates before sampling
      let warpX = x + noise(x * 0.01, y * 0.01) * 50;
      let warpY = y + noise(x * 0.01 + 100, y * 0.01) * 50;
      
      let n = noise(warpX * 0.02, warpY * 0.02);
      let bright = n * 255;
      let idx = (x + y * width) * 4;
      pixels[idx] = bright;
      pixels[idx + 1] = bright * 0.8;
      pixels[idx + 2] = bright * 1.2;
      pixels[idx + 3] = 255;
    }
  }
  updatePixels();
}
```

## Combinations

**Typical role:** distortion — bends and twists coordinate space for organic, flowing forms

**Works beautifully with:**
- **perlin-simplex-noise**: The base noise being warped — domain warping is noise fed into itself
- **fbm-noise**: Warp multiple octaves for complex, layered distortion
- **flow-fields**: Warped coordinates create swirling flow that feels like stirred paint
- **gradient-systems**: Warp gradient coordinates for organic color transitions instead of linear ones

**Creates tension with:**
- grid-layout: Warping destroys grid regularity — which can be exactly the point. Grid + warp = melting structure.
- signed-distance-fields: Warping distorts SDF distances, breaking their mathematical guarantees. Warp before SDF evaluation.

**Medium fit:** watercolor-wash, ceramic-glaze, oil-impasto

**Explore from here:**
- If you like organic distortion → also look at warp-displacement for mesh-based warping
- If you want subtler effect → reduce warp strength and use it just for color variation
- To invent something new → try time-varying domain warping where the warp pattern itself slowly evolves

## Art Blocks examples
- RASTER by itsgalo
- Trichro-matic by MountVitruvius
- Edifice by Ben Kovach
- Naïve by Olga Fradina
- phase by Loren Bednar
