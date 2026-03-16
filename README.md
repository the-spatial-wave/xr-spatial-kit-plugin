# xr-spatial-kit — Claude Code Plugin

Plugin per creare scene WebXR con React Three Fiber, Three.js e Vite.

## Installazione

```bash
claude plugin install ./xr-spatial-kit-plugin
# oppure da GitHub:
claude plugin install github:tuo-user/xr-spatial-kit-plugin
```

## Contenuto

### Skills (attivate automaticamente da Claude)
| Skill | Trigger |
|---|---|
| `new-scene` | "crea scena", "nuova scena", "new scene" |
| `lighting-setup` | "aggiungi luci", "lighting", "rig luci" |
| `scene-texts` | "testi 3D", "scritte", "titolo scena" |
| `audio-player` | "audio", "musica", "sound", "AudioPlayer" |
| `video-panel` | "video", "pannello video", "VideoPanel" |

### Commands (invocabili con /)
| Command | Uso |
|---|---|
| `/new-scene` | Genera `src/scenes/NomeScena.tsx` dal template |

## Stack supportato
- React 18
- @react-three/fiber v8
- @react-three/drei
- @react-three/postprocessing v2 (**non v3**)
- Three.js 0.183+
- Vite + TypeScript

## Compatibilità
Testato su xr-reset-kit-starter — The Spatial Wave.
