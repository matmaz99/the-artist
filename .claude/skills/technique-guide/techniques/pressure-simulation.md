# Stroke Pressure Simulation


## Preview
![pressure-simulation preview](../previews/pressure-simulation.png)

## What it looks like
Lines and strokes that vary in width and opacity along their length, exactly like a pen or brush pressed harder and lighter on paper. The attack (beginning), sustain (middle), and release (end) of each stroke have distinct character — a thin start that swells to full width then tapers off, or a bold entry that fades. The effect reads immediately as hand-drawn because our eyes recognize pressure variation as the signature of human touch.

## How it works
Define a pressure curve along the stroke's normalized length (0 to 1). At each point, the pressure value (0-1) controls both stroke width and opacity. A Gaussian-based profile creates natural pen dynamics: `pressure = exp(-pow((t - peak) / sigma, 2))` where `peak` controls where maximum pressure occurs and `sigma` controls how quickly it tapers. Multiple Gaussian peaks can simulate lifting and re-pressing. The pressure value is then mapped to width (min to max) and alpha (light to full).

## Parameters
- **pressure peak**: where along the stroke maximum pressure occurs (0.2-0.6)
- **sigma**: width of the pressure bell curve — wider = more sustained pressure (0.1-0.5)
- **min width**: stroke width at lightest pressure (0.5-2 px)
- **max width**: stroke width at heaviest pressure (4-20 px)
- **opacity mapping**: how pressure maps to alpha — linear, squared, or threshold (0-1)
- **attack sharpness**: how quickly pressure ramps up at stroke start (0.5-3.0)

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  background(245, 242, 235);
  noLoop(); randomSeed(42); noiseSeed(42);
  noFill();

  for (let s = 0; s < 20; s++) {
    let startX = random(30, 370), startY = random(30, 370);
    let col = color(35 + random(40), 30 + random(30), 25 + random(20));
    let peak = random(0.25, 0.55);
    let sigma = random(0.15, 0.4);
    let maxW = random(3, 14);
    let steps = 80;

    let px = startX, py = startY;
    for (let i = 0; i < steps; i++) {
      let t = i / steps;
      // Gaussian pressure curve
      let pressure = exp(-pow((t - peak) / sigma, 2));
      let w = lerp(0.5, maxW, pressure);
      let a = lerp(20, 180, pressure);

      let nx = px + noise(s, i * 0.05) * 8 - 4;
      let ny = py + noise(s + 100, i * 0.05) * 6 - 3 + 1;

      stroke(red(col), green(col), blue(col), a);
      strokeWeight(w);
      line(px, py, nx, ny);
      px = nx; py = ny;
    }
  }
}
```

## Combinations

**Typical role:** detail / quality — adds human-touch character to any stroke-based technique

**Works beautifully with:**
- **line-drawing**: Pressure transforms mechanical lines into expressive calligraphic marks
- **fat-line-stroke**: Pressure variation on wide strokes creates dramatic thick-thin brush dynamics
- **flow-fields**: Pressure along flow paths simulates a brush that lifts and presses as it follows the current
- **stochastic-brush-rendering**: Pressure modulates scatter radius — light pressure = sparse particles, heavy = dense

**Creates tension with:**
- **grid-layout**: Pressure is inherently gestural; grids are mechanical. Use pressure within grid cells but not on the grid structure itself.

**Medium fit:** fine-pencil, ink-on-paper, charcoal-conte, oil-impasto

**Explore from here:**
- If you like the calligraphic quality → also look at fat-line-stroke, curve-smoothing
- If you want realistic brush dynamics → combine with stochastic-brush-rendering for particle-level pressure response
- To invent something new → try multiple pressure peaks per stroke to simulate hand tremor or rhythm

## Art Blocks examples
- Fidenza by Tyler Hobbs
- Archetype by Kjetil Golid
- Cattails Along the Nile by Jacob Gold
