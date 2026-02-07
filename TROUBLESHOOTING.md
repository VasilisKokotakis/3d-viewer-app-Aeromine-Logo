# Troubleshooting Guide

Common issues and solutions for the 3D Viewer App.

## Model Loading Issues

### Model Not Displaying

**Symptoms**: Page loads but 3D model is blank or shows errors in console

**Solutions**:

1. **Check file path is correct**
   ```jsx
   // Make sure the path is relative to public/
   const { scene } = useGLTF('/models/color_logo.gltf');
   ```

2. **Verify file exists**
   ```bash
   ls -la public/models/
   ```

3. **Check browser console** (Press F12)
   - Look for 404 errors (file not found)
   - Look for CORS errors (if hosted)

4. **Validate glTF file**
   - Use https://gltf-validator.donmccurdy.com/
   - Validator will catch JSON or structural errors

### Texture Not Loading

**Symptoms**: Model appears gray or untextured

**Solutions**:

1. **Check texture URI paths in `.gltf` file**
   ```bash
   grep '"uri"' public/models/your-model.gltf
   ```

   Should output:
   ```json
   "uri":"textures/texture-name.png"
   "uri":"model-name.bin"
   ```

2. **Fix incorrect paths** using sed:
   ```bash
   # Fix texture path
   sed -i 's|"uri":"texture.png"|"uri":"textures/texture.png"|g' public/models/your-model.gltf
   
   # Verify fix worked
   grep '"uri"' public/models/your-model.gltf
   ```

3. **Ensure texture files exist**
   ```bash
   ls public/models/textures/
   ```

### Binary File Not Found

**Symptoms**: Console shows MIME type or 404 errors for `.bin` files

**Solutions**:

1. **Check binary filename in `.gltf`**
   ```bash
   grep '"uri"' public/models/your-model.gltf | grep bin
   ```

2. **Fix mismatched filenames**
   ```bash
   # If GLTF references "Cube%20Services1.bin" but file is "model.bin"
   sed -i 's|"uri":"old-name.bin"|"uri":"actual-name.bin"|g' public/models/your-model.gltf
   ```

3. **Copy/rename the binary if needed**
   ```bash
   cp public/models/old-name.bin public/models/new-name.bin
   ```

## Build & Deploy Issues

### Build Command Fails

**Error**: `npm run build` exits with error

**Solutions**:

1. **Clear dependencies and reinstall**
   ```bash
   rm -rf node_modules package-lock.json
   npm install
   npm run build
   ```

2. **Check Node.js version**
   ```bash
   node --version  # Should be 16+
   npm --version
   ```

3. **Look for syntax errors**
   ```bash
   npm run build 2>&1 | tail -20  # Show last 20 lines
   ```

### Vercel Deployment Fails

**Error**: `ENOENT: no such file or directory, open '/vercel/path0/package.json'`

**Solutions**:

1. **Verify package.json is in repository root**
   ```bash
   git show HEAD:package.json
   ```

2. **Push all files to GitHub**
   ```bash
   git status
   git add .
   git commit -m "fix: add missing files"
   git push
   ```

3. **Check `.gitignore` doesn't exclude package.json**
   ```bash
   grep "package.json" .gitignore  # Should return nothing
   ```

4. **Manually trigger redeploy in Vercel dashboard**

### three-mesh-bvh Deprecation Warning

**Warning**: `three-mesh-bvh@0.7.8: Deprecated due to three.js version incompatibility`

**Solution**: Already fixed in `package.json` with overrides:
```json
"overrides": {
  "three-mesh-bvh": "^0.8.0"
}
```

Run: `npm install` to apply.

## Development Server Issues

### Port 5173 Already in Use

**Error**: `Error: port 5173 is already in use`

**Solutions**:

1. **Use different port**
   ```bash
   npm run dev -- --port 3000
   ```

2. **Kill process using the port** (Linux/Mac)
   ```bash
   lsof -ti:5173 | xargs kill -9
   npm run dev
   ```

3. **Or just restart terminal and try again**

### Hot Module Reload (HMR) Not Working

**Symptoms**: Changes to code don't update in browser

**Solutions**:

1. **Check file saved properly**
   - Ensure VS Code has auto-save enabled
   - Or manually save (Ctrl+S)

2. **Clear browser cache**
   - Hard refresh: Ctrl+Shift+R (or Cmd+Shift+R on Mac)

3. **Restart dev server**
   ```bash
   # Stop: Ctrl+C
   npm run dev
   ```

## Browser Compatibility

### Model Doesn't Render in Older Browsers

**Solution**: Requires WebGL support (Chrome 8+, Firefox 4+, Safari 5.1+, Edge 12+)

Check support: https://caniuse.com/webgl

### Performance Issues / Slow Rendering

**Solutions**:

1. **Reduce model complexity**
   - Works best with < 100k polygons
   - Use LOD (Level of Detail) versions

2. **Optimize textures**
   - Use compressed formats (WebP)
   - Reduce resolution (2048x2048 or lower)

3. **Check browser GPU**
   - Open DevTools → Performance → record
   - Look for high GPU usage or frame drops

## File Organization

### Git Not Tracking Model Files

**Symptoms**: Files deleted from git but still in filesystem

**Solutions**:

1. **Check .gitignore**
   ```bash
   cat .gitignore
   ```

   Should NOT have:
   - `public/`
   - `*.gltf`
   - `*.bin`
   - `*.png`

2. **If accidentally ignored, re-add**
   ```bash
   git rm --cached public/models/
   git add public/models/
   git commit -m "track model files"
   ```

### Backup Corrupted

**Issue**: If model stops working after editing

**Solution**:

1. **Backups are created automatically**
   ```bash
   ls public/models/*.backup
   ```

2. **Restore from backup**
   ```bash
   cp public/models/color_logo.gltf.backup public/models/color_logo.gltf
   ```

## Common sed Commands

Fix multiple issues:

```bash
# Fix all texture paths at once
sed -i 's|"uri":"\.png"|"uri":"textures/.png"|g' public/models/model.gltf

# Fix URL-encoded filenames
sed -i 's|"uri":"Cube%20Services1.bin"|"uri":"proper-name.bin"|g' public/models/model.gltf

# Verify changes
grep '"uri"' public/models/model.gltf
```

## Still Having Issues?

1. **Check browser console** (F12 → Console tab)
   - Copy error messages
   - Screenshot the errors

2. **Validate your model**
   - https://gltf-validator.donmccurdy.com/
   - Or https://gltf-viewer.donmccurdy.com/

3. **Check logs**
   ```bash
   npm run build 2>&1 | grep -i error
   npm run dev 2>&1 | head -50
   ```

4. **Compare with working model**
   - Use `color_logo.gltf` as reference
   - Check file structure matches

---

**If issue persists, collect:**
- Error messages from browser console
- Output of `npm run build`
- File listing of `public/models/`
- Output of `grep '"uri"' public/models/your-model.gltf`
