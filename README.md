# nicolesiggins.com

This is the source code for [nicolesiggins.com](https://www.nicolesiggins.com), a personal website built with [Hugo](https://gohugo.io/) and the [Congo theme](https://github.com/jpanther/congo), using Hugo Modules and deployed via GitHub Actions to GitHub Pages.

## Local Development

Make sure you have [Hugo Extended](https://gohugo.io/getting-started/installing/) installed.

This site is built with Hugo version:

```bash
hugo v0.123.8-5fed9c591b694f314e5939548e11cc3dcb79a79c+extended darwin/amd64 BuildDate=2024-03-07T13:14:42Z VendorInfo=gohugoio
```

To preview the site locally:

### Clone the repo
```bash
git clone https://github.com/nicolelaine/nicolesiggins.com.git
cd nicolesiggins.com
```

### Fetch Hugo module dependencies
```bash
hugo mod tidy
```

### Start the local server
```bash
./serve.sh
```

### Or manually run 
```bash
hugo server --baseURL http://localhost:1313/
```

## Deployment 

This site is automatically deployed to GitHub Pages using a GitHub Actions workflow.

Deployment steps:

Push to the main branch.

GitHub Actions runs hugo and deploys the output in the /public/ folder to the gh-pages branch.

The live site is available at:
https://www.nicolesiggins.com

# Repository Structure

| Folder/File          | Description                                               |
| -------------------- | --------------------------------------------------------- |
| `config/_default/`   | Hugo site configuration files (`config.toml`, etc.)       |
| `content/`           | Website's markdown content                                |
| `layouts/`           | Custom templates and overrides                            |
| `static/`            | Static assets (files, etc)                                |
| `assets/`            | Processed assets                                          |
| `archetypes/`        | Contains content templates for new pages or posts         |
| `serve.sh`           | Helper script to run the site locally                     |
| `CNAME`              | Stores the custom domain                                  |
| `.gitignore`         | Everything not pushed to Git/Github                       |
| `go.mod`, `go.sum`   | Hugo Modules configuration                                |
| `.github/workflows/` | GitHub Actions deployment setup                           |

# Housekeeping

The public/ and resources folders are not committed — they are regenerated automatically.
Unused folders like i18n/, data/, and themes/ were removed for clarity.

# Credits

Theme: Congo by @jpanther
Built with Hugo

