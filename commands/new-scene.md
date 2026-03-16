---
description: Genera src/scenes/NomeScena.tsx dal template xr-reset-kit
argument-hint: <NomeScena>
allowed-tools: Write, Read, Glob
---

Crea un nuovo file scena per il progetto xr-reset-kit-starter.

Il nome della scena è: $ARGUMENTS

## Istruzioni

1. Verifica che `src/scenes/` esista nel progetto corrente
2. Crea il file `src/scenes/$ARGUMENTS.tsx` con questo contenuto esatto:

```tsx
// $ARGUMENTS.tsx
// xr-reset-kit-starter — The Spatial Wave

import { Suspense } from 'react'
import { Particles } from '../components/Particles'
import { NeonArch } from '../components/NeonArch'
import { FloorGlow } from '../components/FloorGlow'
import { Effects } from '../components/Effects'

export function $ARGUMENTS() {
  return (
    <>
      <Effects />

      <color attach="background" args={['#050012']} />
      <fog attach="fog" args={['#180028', 2.7, 9.2]} />

      {/* ── LUCI BASE ── */}
      <ambientLight intensity={0.035} color="#2a1750" />
      <hemisphereLight intensity={0.06} color="#77bfff" groundColor="#0a0012" />
      <directionalLight position={[0, 2.1, 4]} intensity={0.06} color="#e5efff" />

      {/* ── HALO NEON ── */}
      <pointLight position={[0, 1.35, -1.4]} intensity={42} distance={6.5} decay={2} color="#9fefff" />
      <pointLight position={[0, 1.35, -1.6]} intensity={60} distance={7} decay={2} color="#8ff7ff" />

      {/* ── ACCENTI ── */}
      <pointLight position={[-1.0, 0.95, -0.15]} intensity={10} distance={3.2} decay={2} color="#ff45d8" />
      <pointLight position={[1.0, 0.95, -0.15]} intensity={10} distance={3.2} decay={2} color="#3be4ff" />

      {/* ── ELEMENTI SCENA ── */}
      <Particles count={45} />

      <group position={[0, 0.08, -0.52]} scale={0.66}>
        <NeonArch />
      </group>

      <group position={[0, 0.03, 0.02]} scale={0.78}>
        <FloorGlow />
      </group>

      {/* Modello 3D — decommentare quando disponibile */}
      <Suspense fallback={null}>
        {/* <group position={[0, 0.5, 0.18]} scale={1.28}>
          <ModelComponent />
        </group> */}
      </Suspense>
    </>
  )
}
```

3. Comunica all'utente:
   - Il file creato: `src/scenes/$ARGUMENTS.tsx`
   - Come aggiungerlo in `App.tsx`:
     ```tsx
     import { $ARGUMENTS } from './scenes/$ARGUMENTS'
     // dentro <Canvas>: <$ARGUMENTS />
     ```
