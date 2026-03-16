---
name: lighting-setup
description: Use this skill when the user asks to "aggiungi luci", "setup lighting", "rig luci", "illumina la scena", "halo neon", or wants to configure lights for a cyberpunk/neon XR scene.
version: 1.0.0
---

# Lighting Setup — Neon Cyberpunk

## Principio base
La scena deve restare **scura** — le luci neon devono dominare.
- `ambientLight` max intensity `0.05`
- Niente directional forte — solo fill leggero

## Rig completo collaudato

```tsx
{/* Base */}
<ambientLight intensity={0.035} color="#2a1750" />
<hemisphereLight intensity={0.06} color="#77bfff" groundColor="#0a0012" />
<directionalLight position={[0, 2.1, 4]} intensity={0.06} color="#e5efff" />

{/* Halo principale dietro il soggetto */}
<pointLight position={[0, 1.35, -1.4]} intensity={42} distance={6.5} decay={2} color="#9fefff" />
<pointLight position={[0, 1.35, -1.6]} intensity={60} distance={7} decay={2} color="#8ff7ff" />

{/* Accenti magenta / cyan */}
<pointLight position={[-1.0, 0.95, -0.15]} intensity={10} distance={3.2} decay={2} color="#ff45d8" />
<pointLight position={[1.0, 0.95, -0.15]} intensity={10} distance={3.2} decay={2} color="#3be4ff" />

{/* Atmosfera laterale */}
<pointLight position={[-2.0, 0.55, 0.55]} intensity={8} distance={4.6} decay={2} color="#7f2cff" />
<pointLight position={[2.0, 0.55, 0.55]} intensity={8} distance={4.6} decay={2} color="#1edbff" />

{/* Glow pavimento — decay=1 per diffusione larga */}
<pointLight position={[-0.55, 0.08, -0.28]} intensity={3.5} distance={8} decay={1} color="#ff3edb" />
<pointLight position={[0.55, 0.08, -0.28]} intensity={3.5} distance={8} decay={1} color="#32e7ff" />

{/* Key light sul soggetto */}
<spotLight
  position={[0, 2.8, 2.2]}
  target-position={[0, 0.6, 0.18]}
  intensity={55}
  distance={6}
  angle={0.28}
  penumbra={0.85}
  decay={2}
  color="#e8f4ff"
/>
```

## Parametri chiave

| Parametro | Effetto |
|---|---|
| `decay={1}` | Falloff lineare — glow largo sul pavimento |
| `decay={2}` | Falloff fisico — spot puntuale |
| `penumbra={0.85}` | Bordi spot morbidissimi |
| `distance` | Raggio massimo luce (oltre = buio totale) |

## Colori neon collaudati
| Ruolo | Hex |
|---|---|
| Cyan core | `#9fefff` / `#87f7ff` |
| Magenta | `#ff3ed5` / `#ff45d8` |
| Cyan accento | `#32e7ff` / `#3be4ff` |
| Viola atmosfera | `#7f2cff` / `#8d2dff` |
| Key light | `#e8f4ff` |
