# Frequency Drifters - Technical Specification

## Project Overview

- **Project Name:** Frequency Drifters
- **Type:** Zero-Gravity Musical Racing Game
- **Core Functionality:** Players pilot a spaceship through asteroid fields while collecting musical notes that trigger synthesized sounds, building combos through drift mechanics
- **Target Users:** Casual gamers who enjoy rhythm/visualizer games

## Visual & Rendering Specification

### Scene Setup

- **Camera:** Third-person follow camera, positioned behind and above the ship
- **Camera Offset:** `(0, 8, 20)` relative to ship, smooth lerp follow (factor: 0.05)
- **Lighting:**
  - Ambient light: `#1a1a2e` intensity 0.4
  - Directional light: `#ffffff` intensity 1.0, position `(10, 20, 10)`
  - Point lights on notes: colored per note type
- **Environment:** Deep space with subtle star field particle system (500 stars)
- **Fog:** Exponential fog, color `#0a0a1a`, density 0.015

### Materials & Effects

- **Ship Material:** MeshStandardMaterial with metallic blue (`#00d4ff`), roughness 0.3, metalness 0.8
- **Asteroid Material:** MeshStandardMaterial with gray (`#444444`), roughness 0.9, metalness 0.1
- **Note Material:** Emissive MeshBasicMaterial with glow
  - C: Red (`#ff3366`)
  - D: Orange (`#ff9933`)
  - E: Yellow (`#ffff33`)
  - G: Green (`#33ff66`)
  - A: Blue (`#3399ff`)
- **Drift Trail:** Particle system with additive blending, cyan color

### Post-Processing

- **UnrealBloomPass:**
  - Strength: 1.5
  - Radius: 0.4
  - Threshold: 0.2
- **Render Resolution:** Full window, antialias disabled (bloom handles smoothing)

### 3D Assets

- **Spaceship:** Custom geometry (elongated octahedron with fins)
- **Asteroids:** IcosahedronGeometry with noise displacement, 3 size variants (small: 1-2, medium: 3-4, large: 5-8)
- **Musical Notes:** OctahedronGeometry, scale 0.8, rotating animation
- **Drift Particles:** Points geometry, 100 particles, size 0.3

## Simulation Specification

### Physics Type

- Custom zero-G movement (no gravity)
- Velocity-based with damping
- Drift mechanics based on lateral velocity

### Parameters

- **Max Speed:** 50 units/sec
- **Acceleration:** 30 units/sec²
- **Turn Speed:** 2.5 rad/sec
- **Drift Threshold:** Lateral velocity > 8 units/sec triggers drift
- **Damping:** 0.98 (space friction)
- **Drift Damping:** 0.95 (grip loss during drift)

### Asteroid Field

- **Spawn Rate:** Every 0.5 seconds
- **Spawn Distance:** 200 units ahead of ship
- **Despawn Distance:** 50 units behind ship
- **Density:** 3-6 asteroids per spawn wave
- **Lane System:** 5 lanes across X-axis (-40 to 40)

### Note Spawning

- **Spawn Rate:** Every 1.5 seconds
- **Pattern:** Random from pentatonic scale (C, D, E, G, A)
- **Spawn Distance:** 150 units ahead
- **Lifetime:** 10 seconds before despawn
- **Collection Radius:** 3 units

## Interaction Specification

### User Controls

- **W / Arrow Up:** Accelerate forward
- **S / Arrow Down:** Brake/reverse
- **A / Arrow Left:** Turn left
- **D / Arrow Right:** Turn right
- **Space:** Drift (hold while turning)

### Game Mechanics

- **Score:** +100 points per note collected
- **Combo System:**
  - Base multiplier: 1x
  - Each consecutive note adds +0.5x
  - Drift while collecting: +1x bonus
  - Max multiplier: 10x
  - Combo resets after 3 seconds without collection
- **Drift Points:** +10 points per frame while drifting

### Audio (Tone.js)

- **Synth Type:** PolySynth with FM synthesis
- **Note Frequencies:**
  - C4: 261.63 Hz
  - D4: 293.66 Hz
  - E4: 329.63 Hz
  - G4: 392.00 Hz
  - A4: 440.00 Hz
- **Envelope:** Attack 0.02s, Decay 0.1s, Sustain 0.3, Release 0.5s
- **Effects:** Reverb (convolve), Delay (0.25s, 0.3 feedback)
- **Background Drone:** Low frequency oscillator (50Hz), subtle

### UI Elements

- **Score Display:** Top-left, large white text with glow
- **Combo Display:** Below score, shows current multiplier
- **Speed Display:** Bottom-right, horizontal bar
- **Controls Hint:** Bottom-center, fade out after 5 seconds

## Technical Requirements

### Libraries

- Three.js r183 (CDN: https://cdn.jsdelivr.net/npm/three@0.183.0/build/three.module.js)
- Three.js addons: EffectComposer, RenderPass, UnrealBloomPass
- Tone.js v15.1.22 (CDN: https://cdn.jsdelivr.net/npm/tone@15.1.22/build/Tone.js)

### Performance Targets

- 60 FPS on mid-range hardware
- Max 100 asteroids active
- Max 20 notes active
- Object pooling for asteroids and notes

## Acceptance Criteria

1. Ship moves smoothly in zero-G with momentum
2. Asteroids spawn ahead and despawn behind
3. Notes play distinct tones when collected
4. Drift mechanic activates with spacebar + turn
5. Combo multiplier increases with consecutive collections
6. Bloom effect visible on notes and ship
7. Score updates in real-time
8. Game runs at stable 60 FPS
9. All controls responsive
10. Audio plays without crackling
