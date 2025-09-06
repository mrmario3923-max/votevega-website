# Deployment Setup

This project uses GitHub Actions to automatically build and deploy to Surge.sh when changes are pushed to the `main` branch.

## Surge.sh Deployment

The site is deployed to: **https://votevega-beta.surge.sh**

### Required GitHub Secrets

To enable deployment, you need to configure the following secrets in your GitHub repository:

1. Go to your GitHub repository
2. Navigate to **Settings** → **Secrets and variables** → **Actions**
3. Add these repository secrets:

#### `SURGE_LOGIN`
Your Surge.sh account email address.

#### `SURGE_TOKEN`
Your Surge.sh authentication token. Get this by:
```bash
# Install Surge CLI locally
npm install -g surge

# Login to get your token
surge login

# Get your token
surge token
```

### Manual Deployment

You can also trigger a deployment manually:
1. Go to the **Actions** tab in your GitHub repository
2. Select **Build and Deploy to Surge.sh**
3. Click **Run workflow**

### Local Testing Before Deployment

Before pushing to main, test your changes locally:

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production (test the build process)
npm run build

# Serve the built site locally
cd public && python3 -m http.server 8080
```

### Deployment Process

The GitHub Action will:
1. ✅ Check out the repository code
2. ✅ Set up Hugo (latest extended version)
3. ✅ Set up Node.js and install dependencies
4. ✅ Build the site with `npm run build`
5. ✅ Install Surge CLI
6. ✅ Deploy to `votevega-beta.surge.sh`
7. ✅ Display the deployment URL

### Build Performance

- **Hugo Version**: Latest extended (supports SCSS/PostCSS)
- **Build Time**: ~20-30ms (Hugo's lightning-fast builds)
- **Node.js Version**: 20 (LTS)
- **Deployment**: Instant with Surge.sh

### Troubleshooting

#### Build Fails
- Check that all content files have valid YAML frontmatter
- Ensure all templates are properly formatted
- Verify that required images exist in `static/images/`

#### Deployment Fails
- Verify `SURGE_LOGIN` and `SURGE_TOKEN` secrets are set correctly
- Check that the domain `votevega-beta.surge.sh` is available
- Ensure your Surge.sh account has sufficient permissions

#### Site Not Updating
- Check the Actions tab for deployment status
- Verify the deployment completed successfully
- Clear your browser cache or try incognito mode

### Alternative Deployment Options

This workflow can be easily modified for other hosting platforms:

- **Netlify**: Replace Surge step with Netlify CLI
- **Vercel**: Use Vercel CLI and deployment actions
- **GitHub Pages**: Use `peaceiris/actions-gh-pages` action
- **AWS S3**: Use AWS CLI to sync to S3 bucket
- **Firebase Hosting**: Use Firebase CLI deployment
