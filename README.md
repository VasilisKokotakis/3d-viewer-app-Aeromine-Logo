# 3D Viewer App - Aeromine Logo

A modern, interactive 3D model viewer built with React, Three.js, and Vite. Perfect for showcasing 3D assets, product models, and logos in a seamless web experience.

## Features

- **glTF & GLB Support** - Load `.gltf`, `.glb`, and binary model files
- **Interactive Controls** - Rotate, zoom, and pan with intuitive mouse controls
- **Real-time Rendering** - High-quality 3D graphics with proper lighting and materials
- **Responsive Design** - Works seamlessly on desktop and tablet devices
- **Fast Development** - Hot module reloading with Vite
- **Production Ready** - Optimized builds with tree-shaking and code splitting

## Quick Start

### Prerequisites

- Node.js 16+
- npm or yarn

### Installation

```bash
# Clone the repository
git clone https://github.com/VasilisKokotakis/3d-viewer-app-Aeromine-Logo.git
cd 3d-viewer-app-Aeromine-Logo

# Install dependencies
npm install

# Start development server
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

### Build for Production

```bash
npm run build      # Creates optimized build in dist/
npm run preview    # Preview production build locally
```

## Project Structure

```
.
├── public/
│   ├── models/                    # 3D model files and textures
│   │   ├── color_logo.gltf       # Aeromine logo model
│   │   ├── color_logo.bin        # Model binary data
│   │   └── textures/             # Texture files
│   └── index.html
├── src/
│   ├── components/
│   │   ├── Model.jsx             # 3D model component
│   │   └── ModelViewer.jsx       # Viewer container
│   ├── App.jsx                   # Main app component
│   ├── main.jsx                  # Entry point
│   ├── App.css
│   └── index.css
├── ARCHITECTURE.md               # Detailed architecture docs
├── QUICKSTART.md                 # Step-by-step guide
├── TROUBLESHOOTING.md            # Common issues & fixes
├── package.json
├── vite.config.js
└── README.md
```

## Controls

| Action | Input |
|--------|-------|
| **Rotate** | Click and drag with mouse |
| **Zoom** | Mouse wheel up/down |
| **Pan** | Right-click and drag (Ctrl+Click on Mac) |

## Technologies

| Package | Version | Purpose |
|---------|---------|---------|
| React | ^18.3.1 | UI framework |
| Three.js | ^0.170.0 | 3D graphics engine |
| @react-three/fiber | ^8.17.10 | React + Three.js bridge |
| @react-three/drei | ^9.117.3 | 3D utilities & helpers |
| Vite | ^7.3.1 | Build tool & dev server |

## Adding Your Own Models

1. **Place model files in `public/models/`**
   ```bash
   public/models/
   ├── my-model.gltf
   ├── my-model.bin
   └── textures/
       └── texture.png
   ```

2. **Update the model path in [src/components/Model.jsx](src/components/Model.jsx)**
   ```jsx
   const { scene } = useGLTF('/models/my-model.gltf');
   ```

3. **Fix texture paths if needed**
   ```bash
   sed -i 's|"uri":"texture.png"|"uri":"textures/texture.png"|g' public/models/my-model.gltf
   ```

For detailed instructions, see [QUICKSTART.md](QUICKSTART.md).

## Browser Support

| Browser | Minimum Version |
|---------|-----------------|
| Chrome | 90+ |
| Firefox | 88+ |
| Safari | 14+ |
| Edge | 90+ |

Requires WebGL support. Check compatibility: https://caniuse.com/webgl

## Deployment

### Vercel (Recommended)

1. Push to GitHub
2. Connect repository to Vercel
3. Auto-deploys on every push

### Other Platforms

Deploy the `dist/` directory to:
- Netlify
- GitHub Pages
- Firebase Hosting
- AWS S3
- Any static host

## Documentation

- **[QUICKSTART.md](QUICKSTART.md)** - Installation and basic usage
- **[TROUBLESHOOTING.md](TROUBLESHOOTING.md)** - Common issues and solutions
- **[ARCHITECTURE.md](ARCHITECTURE.md)** - Technical architecture details

## Resources

- [Three.js Documentation](https://threejs.org/docs/)
- [React Three Fiber Docs](https://docs.pmnd.rs/react-three-fiber/)
- [Drei GitHub](https://github.com/pmndrs/drei)
- [glTF Specifications](https://www.khronos.org/gltf/)
- [Free 3D Models](https://sketchfab.com/)

## Tips for Best Performance

- Use **`.glb` format** instead of `.gltf` for smaller file sizes
- Keep models under **100k polygons** for smooth performance
- **Optimize textures** - use compressed formats and reasonable resolutions
- Use **LOD (Level of Detail)** versions for complex models
- Test on slower devices to ensure good performance

## Troubleshooting

### Model not showing?
- Check browser console (F12) for errors
- Verify file paths are relative to `public/`
- Use [glTF Validator](https://gltf-validator.donmccurdy.com/) to check model files

### Build fails?
```bash
rm -rf node_modules package-lock.json
npm install
npm run build
```

See [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for more help.

## License

MIT License - Feel free to use this project for personal or commercial purposes.

## Contributing

Contributions are welcome! You can:
- Report bugs via GitHub Issues
- Suggest improvements
- Submit pull requests
- Share your cool models!

## Development

Developed by [Vasilis Kokotakis](https://github.com/VasilisKokotakis)

---

**Ready to get started?** Check out the [QUICKSTART.md](QUICKSTART.md) guide!

Built with React + Three.js
