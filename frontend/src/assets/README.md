# Assets Folder

## Logo Upload Instructions

1. **Place your logo file here** in this `assets` folder
2. **Supported formats**: SVG (recommended), PNG, JPG, WEBP
3. **File name**: `logo.svg` (or `logo.png` if not SVG)
4. **Recommended size**: 
   - SVG: Any size (scales perfectly)
   - PNG: Width 200-400px, Height auto (maintain aspect ratio)

## Current Setup

The Logo component is configured to use:
- **File name**: `logo.svg`
- **Location**: `frontend/src/assets/logo.svg`

If your logo has a different name, update the import in:
`frontend/src/components/Logo.jsx`

Change this line:
```javascript
import logoImage from '../assets/logo.svg?url'
```

To match your file:
```javascript
import logoImage from '../assets/your-logo-name.svg?url'  // for SVG
// or
import logoImage from '../assets/your-logo-name.png'     // for PNG
```

## After Uploading

1. Save your logo file in this folder
2. Make sure the filename matches what's imported in Logo.jsx
3. The logo will automatically appear in the navbar
4. If the image doesn't load, a fallback SVG will show
