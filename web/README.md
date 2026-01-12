# Fluid Port - WebGL Interactive Image Transforms

This is a browser-based port of the Processing animation from `may_9_15_experiment/` using WebGL2 shaders for GPU-accelerated image transforms.

## Features

- **GPU-accelerated transforms**: All image processing runs on the GPU via WebGL2 fragment shaders
- **Interactive controls**: Click and drag on images to set wave transform centers, click sliders to adjust blending
- **Real-time pipeline**: Multiple chained transforms update at 60fps
- **No build step**: Single HTML file with embedded shaders and JavaScript

## Transform Pipeline

The application implements a dataflow graph of image transforms:

1. **Wave Transform** (input → layer 1): Parametric radial distortion based on click position
2. **Color Inversion** (layer 1 → layer 2): RGB channel inversion
3. **Wave Transform** (layer 2 → layer 3): Second wave distortion with different parameters
4. **Blend Transforms** (layers → outputs): Two blend operations mixing different layers

## Controls

### Image Areas (Click/Drag)
- **Bottom-left image**: Click to set wave center for first transform - creates rippling distortion
- **Top-left image**: Click to set wave center for second transform

### Sliders (Click/Drag)
- **Top-right slider**: Controls blend between original image and processed layer (top-right output)
- **Bottom-right slider**: Controls blend between first layer and processed layer (bottom-right output)

Click or drag vertically on the sliders to adjust blend values (bottom = 0%, top = 100%)

## How to Run

### Option 1: Using npx serve (Recommended)
```bash
cd web
npx serve
```
Then open your browser to `http://localhost:3000`

### Option 2: Using Python HTTP server
```bash
cd web
python3 -m http.server 8000
```
Then open your browser to `http://localhost:8000`

### Option 3: Using any local HTTP server
Since this is a single HTML file that loads local images, you need a local server to avoid CORS restrictions. Any HTTP server will work.

### Option 4: Direct file access (may not work)
Some browsers may allow opening `index.html` directly, but most modern browsers will block loading local images due to CORS policies. Use a local server instead.

## Browser Requirements

- WebGL2 support (Chrome 56+, Firefox 51+, Safari 15+, Edge 79+)
- Tested in modern Chrome, Firefox, and Safari

## Technical Details

### Architecture
- **Rendering**: WebGL2 with fragment shaders
- **Double buffering**: Each layer uses two textures (read/write) that swap each frame
- **Viewport rendering**: Direct rendering to multiple canvas regions without intermediate compositing
- **Full-screen quad**: All transforms render to full-screen quads with texture coordinates

### Shaders
1. **Wave Transform Shader**: Implements radial displacement based on distance from click point
2. **Negation Shader**: Inverts RGB channels
3. **Blend Shader**: Linear interpolation (mix) between two textures
4. **Slider Shader**: Procedural UI rendering for slider controls
5. **Copy Shader**: Simple texture display for final canvas output

### Performance
- All pixel operations run on GPU
- Maintains 60fps on most hardware
- Processes 4x 450x450 images + 2 sliders per frame

## Files

- `index.html` - Main application (WebGL2 + JavaScript)
- `Before elections 015.JPG` - Input image
- `*.jpg`, `*.png` - Additional images from original Processing sketch

## Differences from Processing Version

1. **Coordinate system**: WebGL uses normalized texture coordinates (0-1) vs pixel coordinates
2. **Y-axis**: WebGL texture coordinates have origin at bottom-left, adjusted in viewport rendering
3. **Frame timing**: Uses `requestAnimationFrame` for smooth 60fps instead of Processing's `draw()` loop
4. **Color space**: WebGL uses normalized RGB (0-1) vs Processing's 0-255

## Source Code Structure

The Processing code has been translated as follows:
- `MasterConfig` → JavaScript `WebGLApp` class
- `Transform` classes → Fragment shaders
- `DataRectangle` → WebGL textures
- `DataRectangleDynamic` → Double-buffered textures with framebuffers
- `ClickControl` → Mouse event handlers
- `CustomWaveTransform` → Wave fragment shader
- `NegationTransform` → Negation fragment shader
- `SumOf2Transform` → Blend fragment shader
- `NumericControl` → Slider rendering shader + interaction logic

## Troubleshooting

**Images don't load**: Make sure you're using a local HTTP server, not opening the file directly.

**Black screen**: Check browser console for WebGL errors. Ensure your browser supports WebGL2.

**Poor performance**: WebGL2 requires a GPU. Integrated graphics from ~2015+ should work fine.

**Controls not responding**: Make sure you're clicking within the image or slider regions (visible rectangles)
