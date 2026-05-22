# Assets

```
assets/
├── figures/
│   ├── depth_averaging_concept.svg          ← original schematic (not in any paper)
│   ├── joule_heating_6panel.png             ← Fig 4, Electrophoresis 2017
│   ├── ferrofluid_instability_sequence.png  ← Fig 6, Microfluid. Nanofluid. 2015
│   ├── ferrofluid_2017/
│   │   ├── depthavg_138V.png                ← depth-averaged, 138.9 V/cm
│   │   ├── depthavg_202V.png                ← depth-averaged, 202.1 V/cm (threshold)
│   │   └── depthavg_277V.png                ← depth-averaged, 277.8 V/cm
│   └── iceo_particle_comparison.png         ← Fig 2, Phys. Fluids 2017
│
└── videos/
    ├── exp_138V.gif     ← experiment, 138.9 V/cm (stable)
    ├── exp_175V.gif     ← experiment, 175.0 V/cm (threshold)
    ├── exp_277V.gif     ← experiment, 277.8 V/cm (chaotic)
    ├── 2d_50V.gif       ← regular 2D, 50 V/cm
    ├── 2d_60V.gif       ← regular 2D, 60.4 V/cm (2D threshold)
    └── 2d_110V.gif      ← regular 2D, 110 V/cm
```

## Extracting figures from papers

Export directly from your paper PDFs using the snapshot/crop tool at 150+ dpi as PNG. All figures are your own work.

| File | Source |
|---|---|
| `joule_heating_6panel.png` | Fig 4, *Electrophoresis* 2017 |
| `ferrofluid_instability_sequence.png` | Fig 6, *Microfluid. Nanofluid.* 2015 |
| `ferrofluid_2017/depthavg_*.png` | Fig 1b panels, *Sci. Rep.* 2017 |
| `iceo_particle_comparison.png` | Fig 2, *Phys. Fluids* 2017 |

## Converting videos to GIF

```bash
# Crop to T-junction region (adjust crop=W:H:X:Y to your footage), 10 fps, ~400 px wide
ffmpeg -i EXP_138V.avi -vf "crop=480:200:120:80,fps=10,scale=400:-1" -loop 0 assets/videos/exp_138V.gif
ffmpeg -i EXP_175V.avi -vf "crop=480:200:120:80,fps=10,scale=400:-1" -loop 0 assets/videos/exp_175V.gif
ffmpeg -i EXP_277V.avi -vf "crop=480:200:120:80,fps=10,scale=400:-1" -loop 0 assets/videos/exp_277V.gif
ffmpeg -i 2D_50V.avi   -vf "fps=10,scale=400:-1" -loop 0 assets/videos/2d_50V.gif
ffmpeg -i 2D_60V.avi   -vf "fps=10,scale=400:-1" -loop 0 assets/videos/2d_60V.gif
ffmpeg -i 2D_110V.avi  -vf "fps=10,scale=400:-1" -loop 0 assets/videos/2d_110V.gif
```

Target under 3 MB per GIF. If too large: reduce fps to 8, scale to 320 px, or trim to one clean wave cycle.

For `.nd2` Nikon files, export to TIFF stack from NIS-Elements first:
```bash
ffmpeg -framerate 15 -pattern_type glob -i '*.tif' -vf "fps=10,scale=400:-1" -loop 0 output.gif
```
