# Audio-Reactive Visuals

## What it looks like
Visuals that pulse, shift, and respond to music or sound. Shapes dance to beats, colors shift with frequencies, and composition syncs with audio.

## How it works  
Analyze audio using FFT (Fast Fourier Transform) to get frequency data. Map bass, mids, treble, or individual frequencies to visual parameters. Can also use beat detection or amplitude envelopes.

## Parameters
- **FFT bands**: frequency resolution
- **smoothing**: dampen rapid changes
- **mapping**: which frequencies control which visuals
- **gain**: sensitivity to audio input

## Minimal p5.js sketch
```javascript
let mic, fft;

function setup() {
  createCanvas(400, 400);
  mic = new p5.AudioIn();
  mic.start();
  fft = new p5.FFT();
  fft.setInput(mic);
}

function draw() {
  background(0);
  
  let spectrum = fft.analyze();
  noStroke();
  
  for (let i = 0; i < spectrum.length; i++) {
    let x = map(i, 0, spectrum.length, 0, width);
    let h = map(spectrum[i], 0, 255, 0, height);
    fill(i, 100, 255);
    rect(x, height - h, width / spectrum.length, h);
  }
}

// Note: Requires user interaction to start audio in browsers
```

## Combinations

**Typical role:** input / modulation — drives parameters from sound rather than generating visual form directly

**Works beautifully with:**
- **particle-systems**: Particles react to audio — bass drives emission, treble drives velocity
- **temporal-animation**: Sync animation timing to beat detection for rhythmic visuals
- **flow-fields**: Audio amplitude modulates flow field strength — loud = turbulent, quiet = calm
- **gradient-systems**: Map frequency spectrum to color gradients — bass warm, treble cool

**Creates tension with:**
- metadata-driven: Both want to be the master controller. Pick one as primary driver, use the other for subtle variation.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like reactive visuals → also look at physics-simulation for force-driven response
- If you want subtler response → use audio to modulate existing parameters rather than drive them directly
- To invent something new → try audio-driven domain-warping where sound literally bends space

## Art Blocks examples
- AlgoRhythms by Han x Nicolas Daniel
- Memories of Digital Data by Kazuhiro Tanimoto
- Flux by Owen Moore
- Polychrome Music by Rafaël Rozendaal & Danny Wolfers (Legowelt)
- Chimera by mpkoz
