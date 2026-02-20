# Frequency Drifters

A zero-gravity musical racing game built with Three.js and Tone.js.

## Overview

Pilot your spaceship through an asteroid field while collecting musical notes. Each note you collect plays a tone from the pentatonic scale (C, D, E, G, A), creating an endless musical experience. Master drift mechanics to build combo multipliers and maximize your score.

## Controls

| Key | Action |
|-----|--------|
| W / ↑ | Accelerate |
| S / ↓ | Brake/Reverse |
| A / ← | Turn Left |
| D / → | Turn Right |
| Space | Drift (hold while turning) |

## Gameplay

- **Collect Notes:** Gather musical notes to score points and create music
- **Drift:** Hold Space while turning to drift and earn bonus points
- **Build Combos:** Consecutive note collections increase your multiplier (up to 10x)
- **Drift Collection:** Collecting notes while drifting gives an extra +1x bonus

## Features

- 🎵 Pentatonic scale synthesis (C, D, E, G, A)
- ✨ Bloom post-processing effects
- 🌌 Procedural asteroid fields
- 🎮 Zero-G physics with drift mechanics
- 🔊 Tone.js audio synthesis with reverb and delay

## Tech Stack

- [Three.js](https://threejs.org/) r183 - 3D rendering
- [Tone.js](https://tonejs.github.io/) v15.1.22 - Audio synthesis
- WebGL with post-processing

## Play Online

Visit the live game at: [https://nishivector.github.io/frequency-drifters/](https://nishivector.github.io/frequency-drifters/)

## Development

To run locally:

```bash
# Open index.html in a browser
# Or serve with a local server
npx serve .
```

## License

MIT
