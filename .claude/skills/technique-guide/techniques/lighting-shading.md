# Lighting & Shading

## What it looks like
Depth and volume through light and shadow. Forms that look three-dimensional with highlights, gradients, and cast shadows.

## How it works  
Calculate surface normals, then compute light intensity using dot products (Lambertian shading). Add specular highlights with Phong or Blinn-Phong models. Can ray-trace shadows or use ambient occlusion.

## Parameters
- **light position**: 3D location of light source
- **material**: diffuse, specular, shininess properties
- **ambient**: base light level

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400, WEBGL);
}

function draw() {
  background(200);
  
  // Lighting
  ambientLight(50);
  pointLight(255, 255, 255, 200, -200, 200);
  
  // Material
  ambientMaterial(100, 150, 255);
  specularMaterial(255);
  shininess(20);
  
  // Animated sphere
  push();
  rotateY(frameCount * 0.01);
  rotateX(frameCount * 0.007);
  sphere(80);
  pop();
}
```

## Combinations

**Typical role:** atmosphere — adds 3D depth through light, shadow, and surface response

**Works beautifully with:**
- **ray-marching**: Volumetric lighting on ray-marched forms — shadows, ambient occlusion, glow
- **signed-distance-fields**: SDF normals enable proper lighting calculations on 2D shapes
- **texture-synthesis**: Lit surfaces need texture to look real — specular on rough canvas, matte on paper
- **layered-composition**: Light affects layers differently — front lit, back in shadow

**Creates tension with:**
- posterize-quantization: Smooth lighting gradients + posterize = cel-shading. Intentional tension.
- stroke-hatching: Hatching IS a shading technique — using both means hatching density tracks light direction.

**Medium fit:** oil-impasto, ceramic-glaze

**Explore from here:**
- If you like 3D effects → also look at isometric-projection, ray-marching
- If you want subtler depth → use lighting just for edge highlights, not full shading
- To invent something new → try lighting where the light source moves with domain-warping

## Art Blocks examples
- Blind Spots by shaderism
- Bokeh by mpkoz
- Bokeh Lamps by mpkoz
- Box Light Studies by Zach Lieberman
- Box Light Studies: Sculpture by Zach Lieberman
