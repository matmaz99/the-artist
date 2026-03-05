# Ray Marching

## What it looks like
Ethereal 3D volumes like clouds, smoke, or glowing orbs. Soft, organic forms that blend and intersect smoothly.

## How it works  
For each pixel, cast a ray from camera into scene. March along ray in steps, sampling a density or distance field. Accumulate color/opacity. When threshold is reached, stop. Creates volumetric effects.

## Parameters
- **max steps**: ray march iteration limit
- **step size**: march distance per iteration
- **threshold**: density cutoff
- **field function**: defines volume shape

## Minimal p5.js sketch
```javascript
// Ray marching shader (GLSL pseudo-code)
// Vertex shader passes UV to fragment shader

// Fragment shader:
void main() {
  vec2 uv = (gl_FragCoord.xy / u_resolution) * 2.0 - 1.0;
  vec3 rayOrigin = vec3(0, 0, -3);
  vec3 rayDir = normalize(vec3(uv, 1.0));
  
  float t = 0.0;
  for (int i = 0; i < 64; i++) {
    vec3 p = rayOrigin + rayDir * t;
    float d = length(p) - 1.0; // Sphere SDF
    
    if (d < 0.01) {
      gl_FragColor = vec4(1.0, 0.5, 0.2, 1.0);
      return;
    }
    
    t += d; // March by distance to surface
    if (t > 10.0) break;
  }
  
  gl_FragColor = vec4(0.1, 0.1, 0.2, 1.0); // Background
}

// p5.js would load and apply this shader
```

## Combinations

**Typical role:** rendering — creates 3D volumetric forms like clouds, smoke, and organic blobs

**Works beautifully with:**
- **signed-distance-fields**: SDF defines the volumes that ray marching renders
- **domain-warping**: Warp march coordinates for organic, distorted 3D forms
- **lighting-shading**: Volumetric lighting — shadows, glow, ambient occlusion on marched forms
- **fbm-noise**: Noise-modulated SDF creates cloud-like, organic volumes

**Creates tension with:**
- line-drawing: Ray marching produces smooth surfaces; lines are inherently 2D marks. Interesting if lines are projected onto marched surfaces.
- stroke-hatching: Hatching on 3D forms is powerful (cross-contour hatching) but technically demanding.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like 3D rendering → also look at isometric-projection for simpler 3D look
- If you want faster rendering → use signed-distance-fields in 2D instead of full ray marching
- To invent something new → try ray marching where the SDF is defined by an l-systems branching structure

## Art Blocks examples
- Bubble Blobby by Jason Ting
- Flux by Owen Moore
- Gumbo by Mathias Isaksen
- Skulptuur by Piter Pasma
