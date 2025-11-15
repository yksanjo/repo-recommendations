# 🚀 GitHub Repository Setup Guide

## Repository Name Suggestions

Here are some good names for your repository:

1. **repo-recommendations** (Recommended)
   - Clear and descriptive
   - URL: `https://YOUR_USERNAME.github.io/repo-recommendations/`

2. **github-repo-curator**
   - Professional sounding
   - URL: `https://YOUR_USERNAME.github.io/github-repo-curator/`

3. **awesome-repo-finder**
   - Fun and memorable
   - URL: `https://YOUR_USERNAME.github.io/awesome-repo-finder/`

4. **repo-discovery**
   - Simple and clean
   - URL: `https://YOUR_USERNAME.github.io/repo-discovery/`

5. **curated-repos**
   - Direct and clear
   - URL: `https://YOUR_USERNAME.github.io/curated-repos/`

## Quick Setup Steps

### 1. Create GitHub Repository

```bash
# Choose a name (I recommend: repo-recommendations)
REPO_NAME="repo-recommendations"

# Initialize git (if not already)
cd /Users/yoshikondo/awesome-generative-ai/repoboard
git init

# Create and switch to gh-pages branch
git checkout -b gh-pages

# Add files
git add docs/
git add GITHUB_SETUP.md
git commit -m "Initial commit: Repository recommendations interface"

# Add remote (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/$REPO_NAME.git

# Push
git push -u origin gh-pages
```

### 2. Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages**
3. Under **Source**, select:
   - Branch: `gh-pages`
   - Folder: `/docs`
4. Click **Save**
5. Wait 1-2 minutes for deployment
6. Visit: `https://YOUR_USERNAME.github.io/$REPO_NAME/`

### 3. Update README (Optional)

Edit `docs/README.md` and replace:
- `YOUR_USERNAME` with your GitHub username
- `REPO_NAME` with your repository name

## Alternative: Use Main Branch

If you prefer to use the main branch:

```bash
git checkout main
git add docs/
git commit -m "Add repository recommendations"
git push -u origin main
```

Then in GitHub Settings → Pages:
- Source: `main` branch
- Folder: `/docs`

## Custom Domain (Optional)

1. In GitHub Pages settings, add your custom domain
2. Update DNS records as instructed
3. Your site will be available at your custom domain

## Auto-Update Script

To update the site automatically:

```bash
# Update recommendations
python jobs/master_curator.py --recommend --export

# Update docs
cp output/recommendations.html docs/index.html
cp output/scaled_recommendations.json docs/recommendations.json

# Commit and push
git add docs/
git commit -m "Update recommendations"
git push
```

## Troubleshooting

- **404 Error**: Wait 1-2 minutes after enabling Pages
- **Files not showing**: Make sure files are in `/docs` folder
- **Branch issues**: Use `gh-pages` branch or configure in Settings

