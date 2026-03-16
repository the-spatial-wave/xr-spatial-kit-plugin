---
name: audio-player
description: Use this skill when the user asks to "aggiungi audio", "musica di sottofondo", "spatial audio", "AudioPlayer", "sound in scena", "carica audio", or wants to add audio to a Three.js/R3F scene.
version: 1.0.0
---

# AudioPlayer — Audio in scena R3F

## File da creare
`src/components/AudioPlayer.tsx`

## Componente completo

```tsx
// src/components/AudioPlayer.tsx
import { useEffect, useRef } from 'react'
import { useThree } from '@react-three/fiber'
import * as THREE from 'three'

interface AudioPlayerProps {
  url: string
  volume?: number
  loop?: boolean
  autoplay?: boolean
  spatial?: boolean
  position?: [number, number, number]
  refDistance?: number
}

export function AudioPlayer({
  url,
  volume = 0.5,
  loop = true,
  autoplay = true,
  spatial = false,
  position = [0, 1, 0],
  refDistance = 1,
}: AudioPlayerProps) {
  const { camera } = useThree()
  const listenerRef = useRef<THREE.AudioListener | null>(null)
  const soundRef = useRef<THREE.Audio | THREE.PositionalAudio | null>(null)

  useEffect(() => {
    const listener = new THREE.AudioListener()
    camera.add(listener)
    listenerRef.current = listener

    const sound: THREE.Audio | THREE.PositionalAudio = spatial
      ? new THREE.PositionalAudio(listener)
      : new THREE.Audio(listener)

    const loader = new THREE.AudioLoader()
    loader.load(url, (buffer) => {
      sound.setBuffer(buffer)
      sound.setLoop(loop)
      sound.setVolume(volume)
      if (spatial && sound instanceof THREE.PositionalAudio) {
        sound.setRefDistance(refDistance)
      }
      if (autoplay) sound.play()
    })

    soundRef.current = sound

    return () => {
      if (soundRef.current?.isPlaying) soundRef.current.stop()
      camera.remove(listener)
      listener.context.close()
    }
  }, [url])

  if (!spatial) return null

  return (
    <group position={position}>
      <primitive object={soundRef.current ?? new THREE.Object3D()} />
    </group>
  )
}
```

## Uso in scena

### Background ambient (non spaziale)
```tsx
import { AudioPlayer } from '../components/AudioPlayer'

// Dentro la scena:
<AudioPlayer
  url="/audio/ambient.mp3"
  volume={0.4}
  loop
  autoplay
/>
```

### Spatial audio (suono posizionato nello spazio)
```tsx
<AudioPlayer
  url="/audio/effect.mp3"
  spatial
  position={[2, 1, -1]}
  refDistance={2}
  volume={0.8}
/>
```

## File audio
Metti i file in `public/audio/`:
```
public/
└── audio/
    ├── ambient.mp3
    ├── ambient.ogg   ← fallback per Safari
    └── effect.mp3
```

## Formati supportati
| Formato | Supporto |
|---|---|
| `.mp3` | ✅ universale |
| `.ogg` | ✅ Chrome/Firefox |
| `.wav` | ✅ ma file grandi |
| `.webm` | ✅ Chrome |

## Autoplay browser policy
I browser bloccano l'autoplay audio senza interazione utente.
Soluzione: avvia il suono su click/tap:

```tsx
const [started, setStarted] = useState(false)

// Nel DOM (fuori dal Canvas):
<button onClick={() => setStarted(true)}>Enter</button>

// In scena:
{started && <AudioPlayer url="/audio/ambient.mp3" autoplay />}
```

## Hook useAudio (controllo esterno)
Per play/pause/volume dall'esterno del componente, usa `useRef` passato come prop o uno store Zustand.
