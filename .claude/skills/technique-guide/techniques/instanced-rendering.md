# Instanced Rendering

## What it looks like
Thousands or millions of repeated elements rendered efficiently. Massive crowds, forests, or particle clouds that would be slow individually.

## How it works  
WebGL technique: define geometry once, then use instancing to draw it many times with per-instance attributes (position, color, rotation). GPU processes all instances in parallel.

## Parameters
- **instance count**: number of copies
- **per-instance data**: position, scale, color, rotation
- **base geometry**: shared mesh

## Minimal p5.js sketch
```javascript
// Pseudo-code for WebGL instanced rendering
let instancedMesh;

function setup() {
  createCanvas(400, 400, WEBGL);
  
  // In real Three.js:
  // let geometry = new THREE.BoxGeometry(1, 1, 1);
  // let material = new THREE.MeshBasicMaterial();
  // instancedMesh = new THREE.InstancedMesh(geometry, material, 1000);
  
  // Set per-instance transforms
  // for (let i = 0; i < 1000; i++) {
  //   let matrix = new THREE.Matrix4();
  //   matrix.setPosition(random(-100, 100), random(-100, 100), random(-100, 100));
  //   instancedMesh.setMatrixAt(i, matrix);
  // }
}

function draw() {
  background(200);
  
  // Simplified: draw many boxes (not truly instanced in p5.js)
  for (let i = 0; i < 50; i++) {
    push();
    translate(random(-width/2, width/2), random(-height/2, height/2), random(-100, 100));
    box(10);
    pop();
  }
}

// Real instancing requires WebGL APIs or Three.js
```

## Combinations

**Typical role:** performance — renders thousands of repeated elements efficiently

**Works beautifully with:**
- **particle-systems**: Render huge particle counts with GPU instancing
- **webgl-shaders**: GPU-accelerated rendering — instancing is a shader technique
- **circle-packing**: Draw thousands of packed circles efficiently
- **grid-layout**: Render massive grids with per-instance variation

**Creates tension with:**
- erode-dilate: Post-processing morphological ops are expensive on instanced output — apply to the result, not per-instance.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like mass repetition → also look at particle-systems for dynamic instances
- If you want variation → use hash-randomness to give each instance unique properties
- To invent something new → try instancing where each instance runs a slightly different shader variant

## Art Blocks examples
- JIOMETORY [no compute] by samsy
- while true by Lars Wander
