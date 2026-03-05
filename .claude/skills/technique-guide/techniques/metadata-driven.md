# Metadata-Driven Variation

## What it looks like
Variations you don't see in the code but in the outputs—rare features, special modes, or different compositions driven by token properties.

## How it works  
Token metadata (ID, hash, or external traits) controls parameters. Artists map hash ranges to features, creating rarity tiers. Some tokens might be "rare blue" or "legendary animated" based on their data.

## Parameters
- **hash/ID**: unique token identifier
- **feature mapping**: ranges that trigger special modes
- **rarity distribution**: probability of each trait

## Minimal p5.js sketch
```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
  
  let tokenId = 1234; // Simulated token
  let rareFeature = tokenId % 100 < 5; // 5% rare
  
  background(255);
  
  if (rareFeature) {
    fill(255, 215, 0); // Gold for rare
    textSize(32);
    text('RARE', 150, 200);
  }
  
  let shapes = map(tokenId % 1000, 0, 1000, 3, 20);
  for (let i = 0; i < shapes; i++) {
    fill(random(255), random(255), random(255), 150);
    ellipse(random(width), random(height), 30);
  }
}
```

## Combinations

**Typical role:** input / variation — uses external data (token properties, etc.) to drive visual variation

**Works beautifully with:**
- **hash-randomness**: Metadata is the hash seed — deterministic features from token properties
- **color-palettes**: Metadata selects palette — rare tokens get rare palettes
- **weighted-random**: Metadata drives weight distributions for controlled rarity
- **prng-systems**: Metadata seeds the PRNG for reproducible token-specific output

**Creates tension with:**
- audio-reactive: Both want to be the master controller. Pick metadata or audio as primary driver.

**Medium fit:** versatile — adapts to many mediums depending on context

**Explore from here:**
- If you like data-driven art → also look at hash-randomness for deterministic variety
- If you want more subtle influence → use metadata to shift probabilities rather than make hard choices
- To invent something new → try metadata that selects which medium the artwork simulates

## Art Blocks examples
- Alan Ki Aankhen by Fahad Karim
- Naïve by Olga Fradina
- Act of Emotion by Kelly Milligan
- Aerial View by daLenz
- Algobots by Stina Jones
