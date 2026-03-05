# WebGL Shaders

## What it looks like
Smooth, mathematically precise forms with glowing gradients, organic shapes, or abstract patterns. Everything renders in real-time with depth, lighting, and complex visual effects that would be slow in 2D canvas.

## How it works  
WebGL shaders are programs written in GLSL that run directly on the GPU. Vertex shaders position geometry, fragment shaders color every pixel. Artists write mathematical functions to create patterns, apply lighting models, or simulate physics entirely in shader code. The parallel processing makes complex visuals fast.

## Parameters
- **time**: drives animation cycles
- **resolution**: canvas dimensions
- **custom uniforms**: artist-defined parameters like color, scale, complexity

## Minimal p5.js sketch
```javascript
let theShader;

function preload() {
  theShader = loadShader('shader.vert', 'shader.frag');
}

function setup() {
  createCanvas(400, 400, WEBGL);
}

function draw() {
  shader(theShader);
  theShader.setUniform('u_time', millis() / 1000.0);
  theShader.setUniform('u_resolution', [width, height]);
  rect(-width/2, -height/2, width, height);
}

// shader.frag would contain GLSL code like:
// precision mediump float;
// uniform float u_time;
// uniform vec2 u_resolution;
// void main() {
//   vec2 st = gl_FragCoord.xy/u_resolution;
//   gl_FragColor = vec4(st.x, st.y, abs(sin(u_time)), 1.0);
// }
```

## Combinations

**Typical role:** rendering — GPU-accelerated real-time computation for smooth, mathematical forms

**Works beautifully with:**
- **ray-marching**: Shaders render 3D volumes — ray marching is inherently a shader technique
- **domain-warping**: Distort shader coordinates for organic, flowing GPU-rendered patterns
- **signed-distance-fields**: GPU-accelerated SDF rendering for smooth shapes in real-time
- **temporal-animation**: Time uniform drives shader evolution — smooth, continuous animation

**Creates tension with:**
- svg-generation: Shaders produce raster output; SVG is vector. Different output pipelines — choose one.
- particle-systems: Classic particle systems are CPU-based; shaders compute per-pixel. Transform feedback bridges the gap.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like GPU rendering → also look at instanced-rendering for efficient repetition
- If you want to learn → start with signed-distance-fields and domain-warping in a fragment shader
- To invent something new → try compute shaders that generate geometry for traditional rendering

## Art Blocks examples
- 720 Minutes by Alexis André
- Anticyclone by William Mapan
- Blind Spots by shaderism
- Cargo by Kim Asendorf
- Chimera by mpkoz
