# HSB/HSL Color Manipulation

## What it looks like
Color cycling through hues, saturation shifts, or brightness sweeps. You see smooth transitions through the color spectrum or subtle tonal variations.

## How it works  
HSB (Hue, Saturation, Brightness) and HSL separate color from intensity. Artists increment hue values to cycle through colors, or modulate saturation/brightness for effects. Easier than RGB for color manipulation.

## Parameters
- **hue**: 0-360 color wheel position
- **saturation**: 0-100 color intensity
- **brightness/lightness**: 0-100 luminosity

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  colorMode(HSB, 360, 100, 100);
  noLoop();
}

function draw() {
  background(0, 0, 100);
  noStroke();
  
  for (let i = 0; i < 36; i++) {
    let hue = i * 10;
    fill(hue, 80, 90);
    let x = 20 + (i % 6) * 60;
    let y = 50 + floor(i / 6) * 60;
    ellipse(x, y, 50);
  }
}
```

## Combinations

**Typical role:** color / computation — manipulates color through hue/saturation/brightness axes

**Works beautifully with:**
- **color-palettes**: Generate palettes in HSB space — rotate hue, vary saturation and brightness
- **temporal-animation**: Animate hue values for color cycling and chromatic drift
- **gradient-systems**: HSB gradients along hue axis for rainbow transitions
- **perlin-simplex-noise**: Noise drives hue, saturation, or brightness for organic color variation

**Creates tension with:**
- cosine-gradient-palette: Both define color generation strategy. HSB for intuitive control, cosine for mathematical richness.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like color manipulation → also look at cosine-gradient-palette for smooth cycling
- If you want perceptual accuracy → consider OKLAB space (used in the Ambiant shader) instead of HSB
- To invent something new → try HSB where hue is driven by one noise field and brightness by another

## Art Blocks examples
- Colorspace by Tabor Robak
- Fontana by Harvey Rayner | patterndotco
- AlgoRhythms by Han x Nicolas Daniel
- Construction Token by Jeff Davis
- Elevated Deconstructions by luxpris
