# Quick Start Guide

Get your 3D Viewer App running in minutes!

## Prerequisites

- Node.js 16 or higher
- npm or yarn package manager
- Git (for cloning the repository)

## Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/VasilisKokotakis/3d-viewer-app-Aeromine-Logo.git
cd 3d-viewer-app-Aeromine-Logo
```

### Step 2: Install Dependencies

```bash
npm install
```

### Step 3: Start Development Server

```bash
npm run dev
```

The application will be available at `http://localhost:5173`

## Basic Usage

1. **View Models**: The default Aeromine logo model will load automatically
2. **Rotate**: Click and drag with your mouse to rotate the model
3. **Zoom**: Use the mouse wheel to zoom in and out
4. **Pan**: Right-click and drag (or Ctrl+Click on Mac) to pan the camera

## Adding Your Own Models

### 1. Place Model Files

Put your `.gltf`, `.glb`, or `.bin` files in the `public/models/` directory:

```
public/models/
├── your-model.gltf
├── your-model.bin
└── textures/
    └── texture-file.png
```

### 2. Update the Component

Edit [src/components/Model.jsx](src/components/Model.jsx) and change the model path:

```jsx
// Change this path to your model
const { scene } = useGLTF('/models/your-model.gltf');
```

Or use the [ModelViewer.jsx](src/components/ModelViewer.jsx) component if available.

### 3. Verify Texture Paths

If using `.gltf` format, ensure texture paths in the file are relative:

**Before:**
```json
"uri": "Baked.png"
```

**After:**
```json
"uri": "textures/Baked.png"
```

Use this command to fix texture paths:

```bash
sed -i 's|"uri":"YourTexture.png"|"uri":"textures/YourTexture.png"|g' public/models/your-model.gltf
```

## Building for Production

### Create Production Build

```bash
npm run build
```

Output will be in the `dist/` directory.

### Preview Production Build Locally

```bash
npm run preview
```

## Deployment

### Vercel (Recommended)

1. Push to GitHub
2. Connect your repo to Vercel
3. Vercel will auto-detect Vite and deploy on every push

### Other Platforms

The `dist/` directory is a static site. Deploy it to:
- Netlify
- GitHub Pages
- Firebase Hosting
- Any static host

## Troubleshooting

### Model Not Loading

- Check browser console for errors (F12)
- Verify file paths are relative to `public/`
- Ensure texture URIs in `.gltf` files are correct

### Build Fails

```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
npm run build
```

### Port 5173 Already in Use

```bash
npm run dev -- --port 3000
```

## File Structure

```
.
├── public/
│   ├── models/              # Your 3D model files
│   │   ├── *.gltf/*.glb     # Model files
│   │   ├── *.bin            # Binary data
│   │   └── textures/        # Model textures
│   └── index.html
├── src/
│   ├── components/
│   │   ├── Model.jsx        # 3D model component
│   │   └── ModelViewer.jsx  # Viewer container
│   ├── App.jsx
│   ├── main.jsx
│   └── styles/
├── package.json
├── vite.config.js
└── README.md
```

## Resources

- **Three.js Docs**: https://threejs.org/docs/
- **React Three Fiber**: https://docs.pmnd.rs/react-three-fiber/
- **Drei Utilities**: https://github.com/pmndrs/drei
- **glTF Validator**: https://gltf-viewer.donmccurdy.com/
- **Free Models**: https://sketchfab.com/, https://polyhaven.com/

## Performance Tips

- Use `.glb` format instead of `.gltf` for smaller file sizes
- Optimize textures (use compressed formats like WebP)
- Limit polygon count for web models (< 100k triangles recommended)
- Use LOD (Level of Detail) for complex models

## Getting Help

- Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
- See [ARCHITECTURE.md](ARCHITECTURE.md) for detailed setup
- Review browser console for error messages

---

**Happy modeling! 🚀**
