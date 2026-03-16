---
name: scene-texts
description: Use this skill when the user asks about "testi 3D", "scritte nella scena", "titolo", "subtitle", "branding", "SceneTexts", or wants to add/modify text in a Three.js scene using @react-three/drei Text component.
version: 1.0.0
---

# Scene Texts — 3D Text con @react-three/drei

## Regola critica sui font
`troika-three-text` (usato da `<Text>`) supporta solo **TTF, OTF, WOFF** — **NON WOFF2**.

```tsx
// ✅ Corretto
font="https://cdn.jsdelivr.net/npm/@fontsource/orbitron/files/orbitron-latin-700-normal.woff"

// ❌ Sbagliato — "woff2 fonts not supported"
font="https://cdn.jsdelivr.net/npm/@fontsource/orbitron/files/orbitron-latin-700-normal.woff2"
```

## Template SceneTexts.tsx

```tsx
import { Text } from '@react-three/drei'

const ORBITRON_BOLD = 'https://cdn.jsdelivr.net/npm/@fontsource/orbitron/files/orbitron-latin-700-normal.woff'
const ORBITRON_REGULAR = 'https://cdn.jsdelivr.net/npm/@fontsource/orbitron/files/orbitron-latin-400-normal.woff'

export function SceneTexts() {
  return (
    <>
      {/* Titolo */}
      <Text
        font={ORBITRON_BOLD}
        position={[0, 1.6, -0.45]}
        fontSize={0.38}
        letterSpacing={0.02}
        textAlign="center"
        anchorX="center"
        anchorY="middle"
        color="#ffffff"
        outlineWidth={0.01}
        outlineColor="#ffffff"
      >
        TITOLO SCENA
      </Text>

      {/* Sottotitolo */}
      <Text
        font={ORBITRON_REGULAR}
        position={[0, 1.28, -0.45]}
        fontSize={0.17}
        textAlign="center"
        anchorX="center"
        anchorY="middle"
        color="#9feaff"
      >
        Sottotitolo descrittivo
      </Text>

      {/* Branding */}
      <Text
        font={ORBITRON_BOLD}
        position={[0, 0.32, 1.4]}
        fontSize={0.14}
        letterSpacing={0.08}
        textAlign="center"
        anchorX="center"
        anchorY="middle"
        color="#ffffff"
        outlineWidth={0.003}
        outlineColor="#ccf0ff"
      >
        THE SPATIAL WAVE
      </Text>
    </>
  )
}
```

## Outline
- `outlineWidth` grande (es. `0.01`) → testo sfumato/glow
- `outlineWidth` piccolo (es. `0.003`) → bordo netto definito
- Per testo nitido: `outlineWidth={0.002}` + `outlineColor` leggermente diverso dal colore base

## Font CDN pattern
```
https://cdn.jsdelivr.net/npm/@fontsource/[nome-font]/files/[nome-font]-latin-[peso]-normal.woff
```
Esempi pesi: `400` (regular), `700` (bold), `900` (black)

## Font alternativi
| Font | CDN |
|---|---|
| Orbitron | `@fontsource/orbitron` |
| Space Grotesk | `@fontsource/space-grotesk` |
| Inter | `@fontsource/inter` |
| Rajdhani | `@fontsource/rajdhani` |
