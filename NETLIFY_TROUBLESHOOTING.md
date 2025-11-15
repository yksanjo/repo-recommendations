# 🔧 Netlify Drop Troubleshooting Guide

## Common Issues & Solutions

### Issue 1: File Too Large
**Problem**: Netlify Drop has a 100MB limit per file/folder

**Solution**:
```bash
# Check file sizes
cd output
du -sh *

# If JSON is too large, create a smaller version
python3 -c "
import json
with open('scaled_recommendations.json') as f:
    data = json.load(f)
# Keep only top recommendations
for key in data:
    data[key] = data[key][:50]  # Top 50 per category
with open('recommendations_small.json', 'w') as f:
    json.dump(data, f)
"
```

### Issue 2: Wrong File Structure
**Problem**: Netlify needs `index.html` in the root

**Solution**:
```bash
# Use the prepared netlify-deploy folder
./jobs/netlify_deploy.sh

# This creates a clean folder with:
# - index.html (renamed from recommendations.html)
# - recommendations.json (if needed)
# - Proper Netlify config
```

### Issue 3: Browser Upload Issues
**Problem**: Drag & drop not working in browser

**Solutions**:

**A. Use ZIP file**:
```bash
cd netlify-deploy
zip -r ../netlify-deploy.zip .
# Then upload the ZIP file to Netlify Drop
```

**B. Use Netlify CLI**:
```bash
# Install CLI
npm install -g netlify-cli

# Login
netlify login

# Deploy
cd netlify-deploy
netlify deploy --prod
```

**C. Use Netlify Web Interface**:
1. Go to https://app.netlify.com
2. Sign up/login
3. Click "Add new site" → "Deploy manually"
4. Drag folder or upload ZIP

### Issue 4: JavaScript Not Working
**Problem**: Links or interactivity not working

**Solution**: Make sure you're uploading the complete folder, not just the HTML file. The JSON data is embedded in the HTML, so it should work standalone.

### Issue 5: CORS or Security Issues
**Problem**: Browser blocking local file access

**Solution**: This is why we need to deploy - local files have restrictions. Once on Netlify, everything works.

---

## Step-by-Step: Successful Netlify Upload

### Method 1: Clean Folder Upload (Recommended)

```bash
# 1. Prepare clean deployment folder
./jobs/netlify_deploy.sh

# 2. Open Netlify Drop
open https://app.netlify.com/drop

# 3. Drag the 'netlify-deploy' folder
#    (NOT the 'output' folder - use the prepared one)

# 4. Wait for upload (should show progress)

# 5. Get your URL!
```

### Method 2: ZIP Upload

```bash
# 1. Prepare deployment
./jobs/netlify_deploy.sh

# 2. Create ZIP
cd netlify-deploy
zip -r ../netlify-deploy.zip .

# 3. Go to Netlify Drop
# 4. Upload the ZIP file
# 5. Netlify will extract and deploy
```

### Method 3: Netlify CLI (Most Reliable)

```bash
# 1. Install CLI
npm install -g netlify-cli

# 2. Prepare deployment
./jobs/netlify_deploy.sh

# 3. Login to Netlify
cd netlify-deploy
netlify login

# 4. Deploy
netlify deploy --prod

# 5. Get URL from terminal output
```

---

## Alternative: Other Hosting Options

If Netlify continues to have issues, try these:

### 1. Vercel (Very Similar)
```bash
npm install -g vercel
cd netlify-deploy  # or output folder
vercel --prod
```

### 2. GitHub Pages (Most Reliable)
```bash
./jobs/deploy.sh github
# Follow GitHub Pages setup
```

### 3. Surge.sh (Simple)
```bash
npm install -g surge
cd netlify-deploy
surge
```

### 4. Cloudflare Pages
1. Go to https://pages.cloudflare.com
2. Connect GitHub repo or upload files
3. Deploy

---

## Quick Test Before Upload

Test your HTML file locally first:

```bash
cd netlify-deploy  # or output
python3 -m http.server 8000
# Visit: http://localhost:8000
# Test all features work
```

---

## Still Having Issues?

1. **Check browser console** (F12) for errors
2. **Verify file structure** - should have index.html
3. **Try different browser** - Chrome/Firefox/Safari
4. **Check file permissions** - files should be readable
5. **Use CLI instead** - more reliable than drag & drop

---

## Success Checklist

- [ ] HTML file is named `index.html` (or `recommendations.html`)
- [ ] File size is under 100MB
- [ ] All files in same folder
- [ ] Tested locally first
- [ ] Using prepared `netlify-deploy` folder
- [ ] Browser allows file uploads
- [ ] Internet connection is stable

---

## Need More Help?

- Netlify Docs: https://docs.netlify.com
- Netlify Community: https://answers.netlify.com
- Check file in browser first: `file:///path/to/index.html`

