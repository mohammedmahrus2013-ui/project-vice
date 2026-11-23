# Project VICE — Reverse-Engineering Study Notes

This document records the public-source technical study guiding VICE. The goal is to understand systems and independently implement them for our own coastal-city game—not to reproduce proprietary GTA code, maps, characters, audio, or assets.

## Reference projects inspected

- **Overdrive City** — https://github.com/appleweiping/overdrive-city
  - Public repository with an MIT license (reviewed on 2026-11-23).
  - Useful browser-native reference for procedural city generation, vehicle handling, traffic, and rendering efficiency.
- **Defy** — https://github.com/openfw-game/defy
  - Open-source GTA-inspired Godot project. Useful for understanding how an open-world project separates scenes, scripts, and systems.
- **Dream Driver** — https://github.com/evancodez/dreamdriver
  - Three.js procedural island-driving reference.

## Findings from the Overdrive City code study

1. **One shared city representation:** road tiles, building placement, traffic lanes, collision queries, and mission placement should derive from a common city data model. This avoids systems disagreeing about where roads are.
2. **Instancing for scale:** repeated static objects (windows/buildings/lamps/trees/markings) should use merged geometry or InstancedMesh rather than thousands of independent draw calls.
3. **Procedural facade materials:** a reusable window atlas and per-building parameters create visual variety without requiring a unique texture for every building.
4. **Vehicle handling:** split velocity into forward and lateral components; tune lateral grip and handbrake grip separately. This creates controllable slides without pretending the current simple speed/heading controller is realistic physics.
5. **Traffic AI:** cars follow a road/lane graph, choose legal turns at intersections, brake for obstacles, and despawn outside the active simulation radius.
6. **Simulation timing:** use a fixed-step simulation for consistent vehicle/AI behavior, with rendering interpolated separately.

## How VICE will apply these ideas

- Keep the browser target and Three.js renderer.
- Replace the current single-file prototype with modules for city data, city rendering, vehicle dynamics, traffic, pedestrians, camera, and UI.
- Build an original coastal-city road graph and district layout inspired by the requested visual reference.
- Use original procedural geometry/materials and properly licensed third-party assets only.
- Add tests for deterministic city generation, road connectivity, and vehicle update behavior.

## Reverse-engineering workflow

For each system:
1. Observe the visible behavior and define measurable requirements.
2. Inspect public source code and documentation where the license permits.
3. Identify the underlying data structures, update loop, and performance trade-offs.
4. Write an independent implementation and test it in VICE.
5. Record source attribution and comply with the relevant license before adapting any code.

**Important:** Studying an open-source implementation does not make another game's proprietary files or assets free to use. VICE will not extract or redistribute proprietary game assets or code.
