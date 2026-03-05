# L-Systems

## What it looks like
Branching, tree-like or plant-like structures with recursive complexity. Self-similar patterns at multiple scales.

## How it works  
L-system grammar: start with axiom string, replace symbols using production rules, repeat. Then interpret symbols as turtle graphics commands (forward, turn, push/pop state).

## Parameters
- **axiom**: starting string
- **rules**: symbol replacement productions
- **iterations**: recursion depth
- **angle**: branch angle

## Minimal p5.js sketch
```javascript
let axiom = 'X';
let rules = {
  'X': 'F+[[X]-X]-F[-FX]+X',
  'F': 'FF'
};
let sentence = axiom;
let len = 5;
let angle = 25;

function setup() {
  createCanvas(400, 400);
  
  // Generate
  for (let i = 0; i < 4; i++) {
    let next = '';
    for (let char of sentence) {
      next += rules[char] || char;
    }
    sentence = next;
  }
  
  noLoop();
}

function draw() {
  background(255);
  translate(width/2, height);
  stroke(0, 150);
  
  // Turtle graphics interpretation
  let stack = [];
  
  for (let char of sentence) {
    if (char === 'F') {
      line(0, 0, 0, -len);
      translate(0, -len);
    } else if (char === '+') {
      rotate(radians(angle));
    } else if (char === '-') {
      rotate(-radians(angle));
    } else if (char === '[') {
      stack.push({p: createVector(0, 0), a: 0});
      push();
    } else if (char === ']') {
      pop();
      stack.pop();
    }
  }
}
```

## Combinations

**Typical role:** generator — creates branching, recursive structures from grammar rules

**Works beautifully with:**
- **recursive-subdivision**: L-systems define subdivision rules — grammar drives the branching
- **line-drawing**: Render L-system structures as line segments — the classic turtle graphics approach
- **curve-smoothing**: Smooth the angular L-system branches into organic curves
- **noise-density-scatter**: Scatter leaves or flowers at branch endpoints

**Creates tension with:**
- grid-layout: L-systems are branching and organic; grids are rectangular. Interesting if L-system growth is constrained to grid channels.
- symmetry-mirroring: Natural branching has statistical symmetry, not perfect mirror symmetry. Forced symmetry looks artificial.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like branching → also look at differential-growth for freeform organic growth
- If you want botanical accuracy → combine with fat-line-stroke for tapered branch thickness
- To invent something new → try L-systems where the grammar rules change based on fbm-noise at each branch point

## Art Blocks examples
- Ignition by ge1doot
