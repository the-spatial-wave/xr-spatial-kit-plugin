---
name: video-panel
description: Use this skill when the user asks to "pannello video", "carica video", "VideoPanel", "video in scena", "schermo video 3D", "video texture", or wants to display a video on a 3D plane in a Three.js/R3F scene.
version: 1.0.0
---

# VideoPanel — Pannello video 3D in R3F

## File da creare
`src/components/VideoPanel.tsx`

## Componente completo

```tsx
// src/components/VideoPanel.tsx
import { useEffect, useRef, useMemo } from 'react'
import * as THREE from 'three'

interface VideoPanelProps {
  url: string
  position?: [number, number, number]
  rotation?: [number, number, number]
  width?: number
  height?: number
  loop?: boolean
  autoplay?: boolean
  muted?: boolean
  emissiveIntensity?: number
  rounded?: boolean
}

export function VideoPanel({
  url,
  position = [0, 1.5, -1],
  rotation = [0, 0, 0],
  width = 3.2,
  height = 1.8,
  loop = true,
  autoplay = true,
  muted = true,
  emissiveIntensity = 1.2,
}: VideoPanelProps) {
  const videoRef = useRef<HTMLVideoElement | null>(null)

  const texture = useMemo(() => {
    const video = document.createElement('video')
    video.src = url
    video.loop = loop
    video.muted = muted        // muted richiesto per autoplay browser
    video.playsInline = true
    video.crossOrigin = 'anonymous'
    if (autoplay) video.play().catch(() => {})
    videoRef.current = video
    return new THREE.VideoTexture(video)
  }, [url])

  useEffect(() => {
    return () => {
      videoRef.current?.pause()
      texture.dispose()
    }
  }, [texture])

  return (
    <mesh position={position} rotation={rotation}>
      <planeGeometry args={[width, height]} />
      <meshStandardMaterial
        map={texture}
        emissiveMap={texture}
        emissive="#ffffff"
        emissiveIntensity={emissiveIntensity}
        toneMapped={false}
        side={THREE.DoubleSide}
      />
    </mesh>
  )
}
```

## Uso in scena

### Pannello flat (schermo piatto)
```tsx
import { VideoPanel } from '../components/VideoPanel'

<VideoPanel
  url="/videos/promo.mp4"
  position={[0, 1.6, -1.2]}
  width={3.2}
  height={1.8}
/>
```

### Pannello curvo (effetto cinema)
Per un pannello curvo usa `CylinderGeometry` invece di `planeGeometry`:
```tsx
<mesh position={[0, 1.5, 0]}>
  <cylinderGeometry args={[3, 3, 1.8, 32, 1, true, -0.6, 1.2]} />
  <meshStandardMaterial
    map={texture}
    emissiveMap={texture}
    emissive="#ffffff"
    emissiveIntensity={1.2}
    toneMapped={false}
    side={THREE.BackSide}
  />
</mesh>
```

### Aspect ratio comuni
| Formato | width / height |
|---|---|
| 16:9 (landscape) | `3.2 / 1.8` |
| 9:16 (portrait/reel) | `1.0 / 1.78` |
| 1:1 (square) | `2.0 / 2.0` |
| 4:3 | `2.4 / 1.8` |

## File video
Metti i file in `public/videos/`:
```
public/
└── videos/
    ├── promo.mp4
    └── loop.webm    ← fallback più leggero
```

## emissiveIntensity e bloom
Il materiale ha `emissiveMap` = stesso video → il video emette luce.
Con `<Bloom>` attivo, il pannello brillerà come uno schermo reale.

| `emissiveIntensity` | Effetto |
|---|---|
| `0` | Video visibile ma non emissivo |
| `1.0` | Schermo normale |
| `1.5-2.0` | Schermo molto luminoso con bloom |
| `3.0+` | Burn effect — attenzione al bloom |

## Autoplay su mobile
Safari e mobile richiedono `muted={true}` per autoplay.
Per audio nel video, aggiungere un pulsante "Unmute":
```tsx
const [muted, setMuted] = useState(true)
<VideoPanel url="..." muted={muted} />
<button onClick={() => setMuted(false)}>🔊</button>
```
