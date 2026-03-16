---
name: new-scene
description: Use this skill when the user asks to "create a new scene", "add a scene", "nuova scena", "crea scena", or wants to build a new R3F/Three.js scene. Guides creation following xr-reset-kit-starter conventions.
version: 1.0.0
---

# New Scene

## File Location
`src/scenes/SceneName.tsx` — esportata come named function.

## Template

```tsx
// src/scenes/SceneName.tsx
import { Suspense } from 'react'
import { Particles } from '../components/Particles'
import { NeonArch } from '../components/NeonArch'
import { FloorGlow } from '../components/FloorGlow'
import { Effects } from '../components/Effects'

export function SceneName() {
  return (
    <>
      <Effects />

      <color attach="background" args={['#050012']} />
      <fog attach="fog" args={['#180028', 2.7, 9.2]} />

      <ambientLight intensity={0.035} color="#2a1750" />
      <hemisphereLight intensity={0.06} color="#77bfff" groundColor="#0a0012" />
      <directionalLight position={[0, 2.1, 4]} intensity={0.06} color="#e5efff" />

      <pointLight position={[0, 1.35, -1.4]} intensity={34} distance={6.5} decay={2} color="#9fefff" />

      <Particles count={45} />

      <group position={[0, 0.08, -0.52]} scale={0.66}>
        <NeonArch />
      </group>

      <group position={[0, 0.03, 0.02]} scale={0.78}>
        <FloorGlow />
      </group>

      <Suspense fallback={null}>
        {/* <group position={[0, 0.5, 0.18]} scale={1.28}><ModelComponent /></group> */}
      </Suspense>
    </>
  )
}
```

## Registrare in App.tsx
```tsx
import { SceneName } from './scenes/SceneName'
// dentro <Canvas>:
<SceneName />
```

## Regole
- Mai `color="transparent"` — Three.js non lo supporta
- `ambientLight` intensity max 0.1
- Sempre `<Effects />` come primo figlio
