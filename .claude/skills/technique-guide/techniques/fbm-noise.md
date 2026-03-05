# Fractal Brownian Motion (FBM)

## What it looks like
Rich, detailed noise with variation at multiple scales. Looks like natural phenomena—clouds, terrain, or marble.

## How it works  
Fractal Brownian Motion: sum multiple octaves of noise at increasing frequencies and decreasing amplitudes. Each octave adds finer detail. Formula: sum(amplitude^i * noise(frequency^i * x)).

## Parameters
- **octaves**: number of noise layers
- **lacunarity**: frequency multiplier per octave
- **gain**: amplitude multiplier per octave

## Minimal p5.js sketch
```javascript
function fbm(x, y, octaves) {
  let value = 0;
  let amplitude = 1;
  let frequency = 1;
  
  for (let i = 0; i < octaves; i++) {
    value += amplitude * noise(x * frequency, y * frequency);
    frequency *= 2.0; // Lacunarity
    amplitude *= 0.5; // Gain (persistence)
  }
  
  return value;
}

function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  loadPixels();
  for (let x = 0; x < width; x++) {
    for (let y = 0; y < height; y++) {
      let n = fbm(x * 0.005, y * 0.005, 6);
      let bright = n * 255;
      let idx = (x + y * width) * 4;
      pixels[idx] = bright;
      pixels[idx + 1] = bright * 0.9;
      pixels[idx + 2] = bright * 1.1;
      pixels[idx + 3] = 255;
    }
  }
  updatePixels();
}
```

## Combinations

**Typical role:** foundation — provides rich, multi-scale noise that drives everything else

**Works beautifully with:**
- **domain-warping**: Warp FBM coordinates for swirling, turbulent patterns
- **cosine-gradient-palette**: Map FBM output to palette — multi-octave noise creates rich color variation
- **marching-squares**: Extract contour lines from FBM field — topographic map look
- **posterize-quantization**: Quantize FBM into flat bands — creates elevation-like terracing

**Creates tension with:**
- grid-layout: FBM is continuous and smooth; grids are discrete. Use FBM to color/modulate grid cells rather than fighting the structure.

**Medium fit:** watercolor-wash, ceramic-glaze

**Explore from here:**
- If you like layered noise → also look at perlin-simplex-noise for the base primitive
- If you want sharper features → use ridged FBM (absolute value of noise) for mountain-ridge patterns
- To invent something new → try FBM where each octave uses a different noise type

## Art Blocks examples
- Calian by Eric De Giuli
- Pigments by Darien Brito
