# 🌐 How to Share Your Repository Recommendations Publicly

Multiple ways to share your interactive HTML interface with the world!

## Option 1: GitHub Pages (Recommended - Free & Easy)

### Step 1: Create a GitHub Repository

```bash
cd /Users/yoshikondo/awesome-generative-ai/repoboard

# Initialize git if not already done
git init

# Create a gh-pages branch or use main branch
git checkout -b gh-pages
# OR use main branch (GitHub Pages works with both)
```

### Step 2: Prepare Files for GitHub Pages

```bash
# Create a docs folder (or use root)
mkdir -p docs

# Copy the HTML file
cp output/recommendations.html docs/index.html

# Copy the JSON data (if needed for updates)
cp output/scaled_recommendations.json docs/recommendations.json

# Create a README
cat > docs/README.md << 'EOF'
# Repository Recommendations

Interactive, sortable, and filterable repository recommendations.

[View Live Interface](https://YOUR_USERNAME.github.io/REPO_NAME/)
EOF
```

### Step 3: Push to GitHub

```bash
# Add files
git add docs/
git commit -m "Add repository recommendations interface"

# Add remote (replace with your repo URL)
git remote add origin https://github.com/YOUR_USERNAME/REPO_NAME.git
git push -u origin gh-pages
# OR if using main: git push -u origin main
```

### Step 4: Enable GitHub Pages

1. Go to your GitHub repository
2. Click **Settings** → **Pages**
3. Select source branch: `gh-pages` (or `main`)
4. Select folder: `/docs` (or `/root`)
5. Click **Save**
6. Your site will be live at: `https://YOUR_USERNAME.github.io/REPO_NAME/`

**Example URL**: `https://yoshikondo.github.io/repo-recommendations/`

---

## Option 2: Netlify Drop (Easiest - Drag & Drop)

### Step 1: Prepare Files

```bash
cd /Users/yoshikondo/awesome-generative-ai/repoboard/output

# Ensure you have the HTML file
ls -la recommendations.html
```

### Step 2: Deploy

1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag and drop the `output` folder (or just `recommendations.html`)
3. Get instant URL: `https://random-name-123.netlify.app`

**That's it!** No account needed for basic hosting.

### For Custom Domain (Optional)

1. Sign up for free Netlify account
2. Drag & drop your files
3. Go to **Site settings** → **Domain management**
4. Add custom domain

---

## Option 3: Vercel (Fast & Free)

### Using Vercel CLI

```bash
# Install Vercel CLI
npm i -g vercel

# Navigate to output directory
cd /Users/yoshikondo/awesome-generative-ai/repoboard/output

# Deploy
vercel

# Follow prompts, get instant URL
```

### Using Vercel Website

1. Go to [vercel.com](https://vercel.com)
2. Sign up/login
3. Click **Add New Project**
4. Import your GitHub repo or drag & drop files
5. Deploy!

---

## Option 4: Surge.sh (Simple CLI)

```bash
# Install Surge
npm install -g surge

# Navigate to output directory
cd /Users/yoshikondo/awesome-generative-ai/repoboard/output

# Deploy (first time will ask you to create account)
surge

# Follow prompts:
# - Domain: your-name.surge.sh (or random)
# - Project: . (current directory)

# Your site: https://your-name.surge.sh
```

---

## Option 5: Create a Standalone Package

Create a shareable package that others can download and open:

```bash
cd /Users/yoshikondo/awesome-generative-ai/repoboard

# Create shareable package
mkdir -p shareable
cp output/recommendations.html shareable/index.html
cp output/scaled_recommendations.json shareable/recommendations.json

# Create README
cat > shareable/README.md << 'EOF'
# Repository Recommendations

## How to Use

1. Download all files
2. Open `index.html` in your web browser
3. That's it! No server needed.

## Features

- Sortable columns
- Advanced filtering
- Search functionality
- Clickable GitHub links

Generated: $(date)
EOF

# Create ZIP file
cd shareable
zip -r ../repo-recommendations.zip .
cd ..

echo "✅ Shareable package created: repo-recommendations.zip"
```

---

## Option 6: Embed in Existing Website

### Iframe Embed

```html
<iframe 
    src="https://YOUR_URL/recommendations.html" 
    width="100%" 
    height="800px" 
    frameborder="0">
</iframe>
```

### Direct Integration

Copy the HTML content and integrate into your existing site.

---

## Quick Deploy Script

I'll create a script to automate deployment:

```bash
# Save as: deploy.sh
#!/bin/bash

echo "🚀 Deploying Repository Recommendations..."

# Option 1: GitHub Pages
if [ "$1" == "github" ]; then
    echo "📦 Preparing for GitHub Pages..."
    mkdir -p docs
    cp output/recommendations.html docs/index.html
    cp output/scaled_recommendations.json docs/recommendations.json
    echo "✅ Files ready in docs/"
    echo "Now run: git add docs/ && git commit -m 'Deploy' && git push"
fi

# Option 2: Netlify
if [ "$1" == "netlify" ]; then
    echo "📦 Preparing for Netlify..."
    cd output
    echo "✅ Ready! Drag the 'output' folder to netlify.com/drop"
fi

# Option 3: Surge
if [ "$1" == "surge" ]; then
    echo "📦 Deploying to Surge..."
    cd output
    surge
fi

# Option 4: Create ZIP
if [ "$1" == "zip" ]; then
    echo "📦 Creating shareable ZIP..."
    mkdir -p shareable
    cp output/recommendations.html shareable/index.html
    cp output/scaled_recommendations.json shareable/recommendations.json
    cd shareable
    zip -r ../repo-recommendations.zip .
    cd ..
    echo "✅ Created: repo-recommendations.zip"
fi
```

---

## Recommended Workflow

### For Quick Sharing (5 minutes)
1. Use **Netlify Drop** - drag & drop, get URL instantly

### For Permanent Hosting
1. Use **GitHub Pages** - free, reliable, easy updates

### For Custom Domain
1. Use **Netlify** or **Vercel** - both support custom domains

---

## Updating Your Public Site

### GitHub Pages
```bash
# Update files
cp output/recommendations.html docs/index.html

# Commit and push
git add docs/
git commit -m "Update recommendations"
git push
# Site updates automatically in ~1 minute
```

### Netlify/Vercel
- Just drag & drop new files, or
- Connect to GitHub for auto-deploy on push

---

## Tips

1. **Keep JSON Updated**: Include the JSON file for future updates
2. **Add README**: Explain what the interface is
3. **Custom Domain**: Use your own domain for branding
4. **Auto-Update**: Set up GitHub Actions to auto-update daily
5. **Share Link**: Post on social media, forums, etc.

---

## Example URLs

After deployment, you'll get URLs like:
- GitHub Pages: `https://username.github.io/repo-recommendations/`
- Netlify: `https://repo-recommendations.netlify.app`
- Vercel: `https://repo-recommendations.vercel.app`
- Surge: `https://repo-recommendations.surge.sh`

---

## Need Help?

- **GitHub Pages**: [docs.github.com/pages](https://docs.github.com/pages)
- **Netlify**: [docs.netlify.com](https://docs.netlify.com)
- **Vercel**: [vercel.com/docs](https://vercel.com/docs)

