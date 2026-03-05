# Custom PRNG Systems

## What it looks like
Repeatable randomness that looks natural. Same seed produces the same "random" pattern every time. Visually indistinguishable from true randomness, but mathematically deterministic.

## How it works  
Custom pseudo-random number generators (like Xorshift) use mathematical operations to generate sequences that appear random but are deterministic. The seed initializes the state. Common algorithms include Xorshift, Linear Congruential Generator (LCG), and Multiply-with-Carry. Each call advances the internal state and returns a value between 0 and 1.

## Parameters
- **seed**: initial state value that determines the sequence
- **algorithm**: Xorshift, LCG, MWC, etc.
- **state size**: 32-bit, 64-bit, or 128-bit internal state

## Minimal p5.js sketch
```javascript
class Xorshift {
  constructor(seed) {
    this.state = seed || 123456789;
  }
  
  random() {
    this.state ^= this.state << 13;
    this.state ^= this.state >> 17;
    this.state ^= this.state << 5;
    return (this.state >>> 0) / 4294967296;
  }
}

let rng;

function setup() {
  createCanvas(400, 400);
  noLoop();
  rng = new Xorshift(42); // Same seed = same pattern
}

function draw() {
  background(255);
  
  for (let i = 0; i < 100; i++) {
    let x = rng.random() * width;
    let y = rng.random() * height;
    fill(rng.random() * 255, rng.random() * 255, rng.random() * 255);
    ellipse(x, y, 20);
  }
}
```

## Combinations

**Typical role:** utility — provides repeatable random sequences for deterministic artwork generation

**Works beautifully with:**
- **hash-randomness**: Hash seeds the PRNG — different hash = different sequence
- **weighted-random**: PRNG feeds weighted selection — controlled variety from random source
- **metadata-driven**: Metadata provides the seed for token-specific reproducibility
- **particle-systems**: PRNG drives initial positions and velocities reproducibly

**Creates tension with:**
- audio-reactive: Audio input is non-deterministic; PRNG wants determinism. Use PRNG for structure, audio for modulation.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like deterministic art → also look at hash-randomness for position-based randomness
- If you want more variety → use multiple PRNG streams for different aspects (color, position, size)
- To invent something new → try PRNGs with different distributions (Gaussian, Poisson) for different visual qualities

## Art Blocks examples
- Act of Emotion by Kelly Milligan
- Algobots by Stina Jones
- Asemica by Emily Edelman, Dima Ofman, Andrew Badr
- because unless until by ixnayokay
- Elementals by Michael Connolly
