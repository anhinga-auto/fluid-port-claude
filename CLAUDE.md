# Project: Processing → WebGL/JS Port

## Goal
Port the interactive animation in `processing/` to a browser-based version using 
WebGL shaders. The Processing code composes transforms including parametric image warping that 
should run on the GPU via fragment shaders.

## Source code
- `may_9_15_experiment/` contains the original Processing 2.2.1 (Java) code
- Key classes: `MasterConfig`, `Transform`, `CustomWaveTransform`, `DataRectangle`, `DataRectangleDynamic`, etc.
- The transforms are pixel-wise operations ideal for fragment shaders

## Target architecture
- Vanilla JS + WebGL2
- Single HTML file or minimal file structure
- No build step required (can use ES modules via CDN if needed)
- p5.js is acceptable if it simplifies the port, but raw WebGL is fine too

## Key constraints
- Preserve the interactive behavior (mouse/click controls)
- Image transforms should run in shaders, not JS loops
- Include clear instructions for running locally (e.g., `npx serve` or similar)

## Output
Place the web version in `web/` with a README explaining how to run it.
