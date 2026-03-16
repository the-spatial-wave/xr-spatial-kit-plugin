# xr-spatial-kit — Plugin per Claude Code

**Plugin ufficiale di [The Spatial Wave](https://github.com/the-spatial-wave)**

[![GitHub Sponsors](https://img.shields.io/github/sponsors/the-spatial-wave?label=Sponsor&logo=GitHub&color=ff69b4)](https://github.com/sponsors/the-spatial-wave)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Plugin-blueviolet)](https://github.com/the-spatial-wave/xr-spatial-kit-plugin)

Un plugin per Claude Code che ti aiuta a costruire scene WebXR con React Three Fiber, Three.js e Vite — più velocemente, senza dover ricordare ogni parametro a memoria.

> Se questo plugin ti è utile, considera di supportare il progetto tramite [GitHub Sponsors](https://github.com/sponsors/the-spatial-wave) ☕

---

## Cos'è

`xr-spatial-kit` è un set di **skills** e **comandi** per Claude Code pensato per chi crea esperienze 3D e XR. Ogni skill guida Claude nella creazione di componenti specifici — luci, testi, audio, video — seguendo le convenzioni collaudate del progetto [xr-reset-kit-starter](https://github.com/the-spatial-wave/xr-reset-kit-starter).

---

## Installazione

```bash
claude plugin install github:the-spatial-wave/xr-spatial-kit-plugin
```

---

## Cosa include

### Skills
Le skills si attivano **automaticamente** quando parli con Claude — non devi fare nulla, Claude le riconosce dal contesto.

| Skill | Quando si attiva | Cosa fa |
|---|---|---|
| `new-scene` | "crea scena", "nuova scena" | Template completo per una nuova scena R3F |
| `lighting-setup` | "aggiungi luci", "rig luci" | Rig luci neon cyberpunk collaudato |
| `scene-texts` | "testi 3D", "scritte", "titolo" | Guide per `<Text>` con font CDN |
| `audio-player` | "aggiungi audio", "musica" | Componente `AudioPlayer` con spatial audio |
| `video-panel` | "pannello video", "carica video" | Componente `VideoPanel` con VideoTexture |

### Comandi slash
I comandi si invocano manualmente con `/`.

| Comando | Uso | Descrizione |
|---|---|---|
| `/new-scene` | `/new-scene NomeScena` | Genera automaticamente `src/scenes/NomeScena.tsx` |

---

## Guida rapida

### 1. Creare una nuova scena

Digita a Claude:
> "crea una nuova scena chiamata GalleryScene"

Oppure usa il comando diretto:
```
/new-scene GalleryScene
```

Claude creerà `src/scenes/GalleryScene.tsx` con il template completo: luci, arco neon, pavimento, particles e struttura pronta per aggiungere il tuo modello 3D.

---

### 2. Aggiungere audio di sottofondo

Digita a Claude:
> "aggiungi una musica ambient alla scena"

Claude userà la skill `audio-player` e creerà il componente `AudioPlayer.tsx` con il codice completo. Poi basterà:

```tsx
// Metti il file in public/audio/ambient.mp3
<AudioPlayer url="/audio/ambient.mp3" volume={0.4} loop autoplay />
```

> **Nota:** I browser bloccano l'autoplay senza interazione utente. Usa un pulsante "Enter" per avviare l'audio al primo click.

---

### 3. Aggiungere un pannello video

Digita a Claude:
> "aggiungi un pannello video nella scena"

Claude creerà il componente `VideoPanel.tsx`. Uso:

```tsx
// Metti il file in public/videos/promo.mp4
<VideoPanel
  url="/videos/promo.mp4"
  position={[0, 1.6, -1.2]}
  width={3.2}
  height={1.8}
/>
```

Il pannello ha materiale emissivo — con il Bloom attivo brillerà come uno schermo reale.

---

### 4. Configurare le luci

Digita a Claude:
> "aggiungi un rig luci neon alla scena"

Claude userà la skill `lighting-setup` con i valori collaudati: halo dietro il soggetto, accenti magenta/cyan, glow sul pavimento e key spotlight frontale.

---

### 5. Testi 3D

Digita a Claude:
> "aggiungi un titolo e un sottotitolo nella scena"

Claude userà la skill `scene-texts` con font Orbitron caricato da CDN (`.woff` — formato corretto per troika-three-text).

---

## Stack supportato

| Libreria | Versione |
|---|---|
| React | 18 |
| @react-three/fiber | v8 |
| @react-three/drei | ^9 |
| @react-three/postprocessing | **v2** (non v3) |
| Three.js | 0.183+ |
| Vite | 5+ |
| TypeScript | 5+ |

> **Importante:** `@react-three/postprocessing v3` richiede React 19 e fiber v9. Con React 18 usa obbligatoriamente la v2.

---

## Errori comuni risolti da questo plugin

| Errore | Causa | Fix |
|---|---|---|
| `Cannot read properties of undefined (reading 'length')` | postprocessing v3 con React 18 | Downgrade a v2 |
| `woff2 fonts not supported` | troika non supporta woff2 | Usa `.woff` |
| `THREE.Color: Unknown color transparent` | `<color args={['transparent']}>` | Usa un hex es. `#000000` |
| `THREE.Clock: deprecated` | Three.js r168+ | Warning innocuo, usa THREE.Timer |

---

## Progetto base

Questo plugin è pensato per funzionare con **xr-reset-kit-starter**:

```bash
git clone https://github.com/the-spatial-wave/xr-reset-kit-starter
cd xr-reset-kit-starter
npm install
npm run dev
```

---

## Licenza

MIT — [The Spatial Wave](https://github.com/the-spatial-wave)
