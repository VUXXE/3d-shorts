# 3d-shorts

An AI agent skill and rendering kit to generate vertical (9:16) animated cartoon shorts from voiceover audio.

It renders 2D canvas-drawn cartoon characters in a 3D Three.js environment using headless Chromium (Playwright), complete with procedural textures, camera motion, depth-of-field, ink outlines, synthesized music, and sound effects.

---

## Features

- **Vertical 9:16 Format**: Designed specifically for TikTok, YouTube Shorts, and Instagram Reels (1080x1920, 30 fps).
- **Headless Three.js Rendering**: Runs in Chromium via Playwright; supports hardware GPU acceleration or software rendering without Remotion.
- **Audio-Synced Timing**: Aligns character animation and camera actions directly to speech pauses and timestamps.
- **Automated Sound Mix**: Generates synchronized music stems and SFX, automatically balanced against the voice track.
- **Pre-Configured Architecture**: Includes procedural world builders, toon shaders, character card drawing, and QA utilities.

---

## Directory Structure

```text
3d-shorts/
├── SKILL.md                 # Agent skill instructions and workflow definition
├── README.md                # Project documentation
├── .gitignore               # Ignored build and media files
└── kit/
    ├── README.md            # Kit technical summary
    ├── engine/              # Core Three.js render engine, shaders, and painters
    │   ├── index.html       # Web harness
    │   ├── main.js          # Three.js scene, toon materials, and passes
    │   ├── motion.js        # Camera interpolation and animation helpers
    │   ├── paint.js         # Canvas texture generators
    │   └── roman.js         # Character card rendering routines
    ├── example/             # Reference implementation
    │   └── soldier/         # Example story setup and audio cue table
    ├── tools/               # Command-line build and rendering scripts
    │   ├── finish.sh        # Video encoding and loudness QA
    │   ├── render.mjs       # Headless frame renderer
    │   ├── setup.sh         # Project initialisation helper
    │   ├── sheet.py         # Contact sheet generator
    │   └── timing.py        # Voiceover alignment and phrase timing
    └── vendor/
        └── toon.ts          # Pen & character drawing library
```

---

## Prerequisites

- **Node.js**: >= 22.6 (with native TypeScript type stripping)
- **Python**: 3.9+ with `numpy` and `Pillow`
- **FFmpeg**: for audio/video assembly and encoding
- **Playwright**: Chromium browser installed (`npx playwright install chromium`)

---

## Quick Start

1. Initialize a new project directory using the setup script:
   ```bash
   bash kit/tools/setup.sh ~/shorts/my-first-short
   cd ~/shorts/my-first-short
   ```

2. Place your voiceover file (`voice.mp3`) and narration script (`script.txt`) in the project directory, then generate phrase timings:
   ```bash
   python3 timing.py voice.mp3 script.txt --out work
   ```

3. Configure your shot list and camera movements in `web/story.js` and audio cues in `audio.py`.

4. Generate a contact sheet to verify visual staging:
   ```bash
   node render.mjs stills/preview "10,50,100,150"
   python3 sheet.py stills/preview stills/sheet.jpg
   ```

5. Render all frames and compile the final short:
   ```bash
   node render.mjs frames "0-600"
   bash finish.sh "My First Short"
   ```

Output video will be saved in `out/`.

---

## Credits & License

- Based on [mromidev/claude-animated-shorts](https://github.com/mromidev/claude-animated-shorts) (MIT License).
- Released under the [MIT License](LICENSE).
