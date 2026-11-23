# Project VICE — GTA V Reverse-Engineering Research

Our reference target is **Grand Theft Auto V**: its sense of scale, dense city, vehicle feel, world simulation, lighting, missions, and cinematic presentation. VICE remains an original game with its own city, vehicles, characters, missions, code, and assets.

This is a research notebook, not a claim that we have Rockstar's source code or can recreate RAGE exactly. We study public research, documented behavior, and permitted tools, then implement original systems.

## GTA V-focused public research references

- **GTAV-Research** — https://github.com/SoosyBoosy/GTAV-Research
  - Public RAGE/GTA V research repository containing hashes, structures, browser/hook/tool research.
  - Its repository declares GPL-2.0. Treat it as a research reference; review the exact licence and provenance of any component before considering code reuse.
- **GTA V Under the Hood** — https://github.com/Goodvibes74/gta5-under-the-hood
  - Written research guides about GTA V's engine, scripts, physics, AI, missions and single-player systems. The project describes itself as a public reference for modders and says it does not bundle game files or code.
- **OpenRAGE** — https://github.com/Two-Play/openrage
  - Open-source RAGE archive explorer/modding toolkit. Its documentation describes inspection of models, textures, audio, animation, metadata, collisions, paths, cutscenes and scripts from a user's own game installation. It does not supply Rockstar game files. Its code is GPL-3.0-only; it is a separate tool, not a runtime dependency for VICE.
- **GTA V recompiled research** — https://github.com/andrewnakas/gtav-recomp
  - Technical reference for recompilation and platform/runtime work. Its own project documentation explicitly warns that generated game code and assets remain Rockstar copyrighted material and must not be redistributed. VICE will not use or distribute recompiled GTA V code.
- **Overdrive City** — https://github.com/appleweiping/overdrive-city
  - MIT-licensed browser-game reference for Three.js city rendering, vehicle handling, traffic and procedural city architecture.

## What we want to understand from GTA V

1. **World structure and streaming:** how large worlds are partitioned, how nearby content receives detail, and how distant content uses lower detail or is unloaded.
2. **Vehicles:** acceleration, braking, traction, suspension feel, steering response, collision response, damage states and camera behavior.
3. **World population:** traffic lanes, intersections, vehicle spawning, pedestrian navigation, reactions and simulation distance.
4. **Rendering:** material response, time-of-day lighting, atmospheric fog, reflections, shadows, level of detail and post-processing.
5. **Mission architecture:** objectives, triggers, checkpoints, scripted sequences, fail/retry states and rewards.
6. **Audio and feedback:** engine layers, tire/skid feedback, environment ambience and UI response, using original or properly licensed sounds.

We must distinguish measured observations from guesses. Each finding should record its source, game/version context where relevant, confidence, and what VICE can independently implement.

## VICE implementation plan

### Stage 1 — Vehicle feel
Replace the current simple heading/speed movement with a proper vehicle model: forward/lateral velocity, grip, handbrake drift, acceleration curves, braking, suspension movement, wheel rotation and collision response. Tune it against observed driving behavior, not copied code.

### Stage 2 — City and streaming
Build an original coastal city from a road graph and district data. Use instanced architecture, facade materials, road markings, props, and distance-based LOD. Stream city chunks around the player and keep collision data consistent with visible roads.

### Stage 3 — Living city
Add lane-aware traffic, intersection decisions, obstacle avoidance, pedestrian navigation, crossing behavior, and distance-based simulation.

### Stage 4 — Visual quality
Add physically based materials, better vehicle meshes, environment reflections, shadow tuning, day/night cycle, weather, atmospheric perspective, and cinematic camera effects.

### Stage 5 — Gameplay
Add enterable vehicles, on-foot movement, mission triggers, wanted/pursuit behavior, save data, and original story content.

## Legal and technical boundaries

- No proprietary Rockstar source code, decompiled code, generated recompilation output, maps, models, textures, audio, scripts, or other game assets in VICE.
- Do not bypass DRM or access controls. Use a legitimately obtained copy and documented modding tools only where permitted by applicable terms and law.
- Public availability does not automatically mean code is reusable. Check each repository's exact licence, provenance, dependencies, and attribution requirements.
- A tool's licence does not grant rights to the game data it can inspect.
- Reverse engineering is a learning method, not a shortcut that turns a browser prototype into a complete GTA-scale game.

## Research workflow

For every target system:
1. Define the behavior we want to understand.
2. Collect public documentation, permitted observations, and licensed research references.
3. Separate confirmed facts from hypotheses.
4. Design an original VICE implementation.
5. Test it, measure performance, and record the result and source attribution.

**The ambition:** make Project VICE a substantial, polished open-world game inspired by the technical ambition of GTA V—while making it independently.
