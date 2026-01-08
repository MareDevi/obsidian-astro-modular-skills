---
name: astro-modular
description: Optimize Obsidian content for Astro Modular blog theme. Use when working with Astro Modular projects, creating content for astro-modular themes, configuring astro-modular settings, or when the user mentions Astro Modular, Vault CMS, blog publishing, or theme customization.
---

# Astro Modular Skill

This skill enables Claude Code to create optimized content and configurations for Astro Modular, a sophisticated Astro-based blog theme designed specifically for Obsidian users.

## Overview

Astro Modular is a production-ready blog theme that transforms Obsidian into a powerful CMS for instant web publishing. It bridges the gap between personal knowledge management and public web content, with deep integration into Obsidian's workflow.

### Key Features

- **Vault CMS Integration**: Seamless Obsidian-to-web publishing
- **Wikilinks Support**: `[[Internal Links]]` work seamlessly in posts
- **Obsidian Callouts**: Full support for `> [!note]`, `> [!tip]`, `> [!warning]`
- **Theme System**: 17+ built-in themes with custom theme support
- **Command Palette**: Ctrl+K fuzzy search across all content
- **Graph View**: Interactive D3.js force-directed graph of content connections
- **Content Types**: Posts, pages, projects, documentation, and special pages
- **Performance**: Image optimization, reading time calculation, SEO features
- **Feature Toggles**: Every feature can be enabled/disabled independently

### Architecture

Astro Modular is built on:
- **Astro**: Modern static site generator
- **Vault CMS**: Obsidian vault content management
- **Tailwind CSS**: Utility-first CSS framework
- **D3.js**: Interactive graph visualization
- **TypeScript**: Type-safe configuration and components

## Installation

### Prerequisites

1. **Obsidian**: Install Obsidian app
2. **Node.js**: Install Node.js 18+ for Astro
3. **Git**: For version control and deployment

### Setup Steps

1. **Clone Astro Modular**:
```bash
git clone https://github.com/davidvkimball/astro-modular.git
cd astro-modular
npm install
```

2. **Configure Vault CMS**:
   - Open `src/config.ts`
   - Set `vaultPath` to your Obsidian vault path
   - Configure content collections to match your vault structure

3. **Local Development**:
```bash
npm run dev
# Open http://localhost:4321
```

4. **Build for Production**:
```bash
npm run build
# Output in /dist directory
```

5. **Deploy**:
   - Netlify: Connect repository, auto-deploy on push
   - Vercel: Connect repository, auto-deploy on push
   - GitHub Pages: Use `./dist` as publishing source

## Content Types

Astro Modular supports five main content types, each with specific frontmatter requirements and behaviors.

### Posts (Blog Articles)

Posts are blog articles displayed in reverse chronological order with full markdown rendering.

**Location**: `/content/posts/` or `/posts/` folder-based structure

**Required Frontmatter**:
```yaml
---
title: "My Blog Post"
description: "A brief summary for SEO and preview"
date: 2024-01-15
---
```

**Optional Frontmatter**:
```yaml
---
tags: ["javascript", "astro"]
draft: true
image: "posts/my-post/cover.jpg"
imageOG: true
imageAlt: "Alt text for accessibility"
hideCoverImage: false
targetKeyword: "main topic"
---
```

**Features**:
- Wikilinks render correctly (posts only)
- Callouts supported in all content types
- Folder-based asset organization
- Reading time auto-calculated
- SEO metadata auto-generated

### Pages (Static Content)

Pages are static content like About, Contact, or custom pages.

**Location**: `/content/pages/` or `/pages/` folder-based structure

**Required Frontmatter**:
```yaml
---
title: "About Me"
description: "Personal information and background"
date: 2024-01-15
---
```

**Optional Frontmatter**:
```yaml
---
image: "pages/about/profile.jpg"
imageAlt: "Profile photo"
showTOC: false
---
```

**URL Mapping**: Pages map to simple URLs:
- `/pages/about` → `/about`
- `/pages/contact` → `/contact`

### Projects (Portfolio)

Projects showcase portfolio items with repository and project links.

**Location**: `/content/projects/` or `/projects/` folder-based structure

**Required Frontmatter**:
```yaml
---
title: "My Project"
description: "Project description and goals"
categories: ["web", "tools"]
---
```

**Optional Frontmatter**:
```yaml
---
repositoryUrl: "https://github.com/user/repo"
projectUrl: "https://project-demo.com"
status: "in-progress"  # or "completed"
featured: true
image: "projects/my-project/preview.jpg"
---
```

### Documentation (Docs)

Documentation pages with sidebar navigation and versioning support.

**Location**: `/content/docs/` or `/docs/` folder-based structure

**Required Frontmatter**:
```yaml
---
title: "Getting Started"
category: "User Guide"
order: 1
---
```

**Optional Frontmatter**:
```yaml
---
version: "2.0"
showTOC: true
featured: false
---
```

**Features**:
- Sidebar navigation by category
- Table of contents auto-generated
- Version-aware documentation
- Link to headings preserved

### Special Pages

Special pages have reserved URLs and specific purposes.

**Available Special Pages**:
- `/special/home` → `/` (Homepage)
- `/special/404` → `/404` (Custom 404 page)

**Required Frontmatter**:
```yaml
---
title: "Home"
description: "Welcome to my site"
date: 2024-01-15
---
```

## URL Mapping System

Astro Modular transforms Obsidian file paths to web URLs automatically.

### URL Transformation Rules

| Obsidian Path | Web URL |
|--------------|----------|
| `/posts/my-post/index.md` | `/posts/my-post` |
| `/posts/my-post.md` | `/posts/my-post` |
| `/pages/about/index.md` | `/about` |
| `/pages/about.md` | `/about` |
| `/special/home/index.md` | `/` |
| `/index.md` | `/` |

### Anchor Links

Headings and block references are preserved:
- Obsidian: `[[Post#Section]]` → Web: `/post#section`
- Obsidian: `[[Post#^block]]` → Web: `/post#block`

### Asset Path Handling

Images and attachments reference properly:
- Folder-based: `post/image.jpg` → `/post/image.jpg`
- Absolute paths: `/assets/logo.png` → `/assets/logo.png`
- Attachments subfolder: `attachments/photo.jpg` → `attachments/photo.jpg`

## Asset Management

### Folder-Based Organization

Astron Modular supports co-locating assets with content:

```
content/
  posts/
    my-first-post/
      index.md
      cover.jpg
      diagram.png
    another-post.md
    another-post/
      screenshot.png
  pages/
    about/
      index.md
      profile.jpg
```

### Image Optimization

Images are automatically optimized:

1. **Format**: WebP priority, JPEG fallback
2. **Responsive**: Multiple sizes generated
3. **Lazy Loading**: Images load as needed
4. **Naming**: Use SEO-friendly filenames (e.g., `astro-modular-theme.jpg` not `img123.jpg`)

### Asset Sync

Run asset synchronization after adding files:

```bash
npm run sync-images
```

This copies assets from content folders to public directory with optimizations.

## Configuration System

Astro Modular uses a comprehensive configuration system in `src/config.ts`.

### Core Site Settings

```typescript
export const siteConfig = {
  siteUrl: 'https://your-site.com',
  title: 'My Blog',
  description: 'Thoughts and tutorials',
  author: 'Your Name',
  language: 'en',
  dir: 'ltr',  // or 'rtl'
  trailingSlash: false,
}
```

### Theme Configuration

```typescript
export const siteConfig = {
  theme: 'minimal',  // See theme list below
  customTheme: '',    // Path to custom theme file
  font: {
    heading: 'Inter',
    body: 'Inter',
    mono: 'Fira Code',
    source: 'google',  // or 'local', 'none'
  },
}
```

### Content Settings

```typescript
export const siteConfig = {
  postsPerPage: 10,
  showReadingTime: true,
  showTags: true,
  showRelatedPosts: true,
  tocMinDepth: 2,
  tocMaxDepth: 3,
}
```

### Feature Toggles

```typescript
export const siteConfig = {
  commandPalette: true,
  graphView: true,
  darkMode: true,
  comments: false,
  footer: true,
  profilePicture: true,
}
```

## Theme System

### Built-in Themes (17+ Themes)

| Theme | Style | Best For |
|-------|-------|----------|
| `minimal` | Clean, minimal | Professional blogs |
| `oxygen` | Light, airy | Personal blogs |
| `atom` | Dark, IDE-like | Developer blogs |
| `ayu` | Modern, colorful | Creative sites |
| `catppuccin` | Pastel, smooth | Minimalist design |
| `dracula` | Dark, popular | Developer content |
| `nord` | Cool, arctic | Clean aesthetics |
| `solarized` | Balanced, warm | Long-form content |
| `tokyo-night` | Dark, vibrant | Gaming/tech blogs |
| `github` | Familiar, clean | Documentation |
| `monokai` | Dark, contrast | Code-focused |
| `one-dark` | VSCode style | Developer blogs |
| `palenight` | Soft, dark | Aesthetic sites |
| `papercolor` | Light, subtle | Reading-focused |
| `snazzy` | Colorful, bold | Modern design |
| `vaporwave` | Retro, neon | Creative projects |

### Custom Themes

Create custom theme in `src/themes/custom/your-theme.ts`:

```typescript
export default {
  name: 'Your Theme',
  colors: {
    background: '#ffffff',
    foreground: '#000000',
    primary: '#3b82f6',
    accent: '#8b5cf6',
    // ... more color tokens
  },
  fonts: {
    heading: 'Your Font',
    body: 'Your Font',
  },
}
```

Activate in `src/config.ts`:

```typescript
theme: 'your-theme',
```

## Feature Toggles

Every feature can be independently enabled or disabled in `src/config.ts`.

### Content Features

```typescript
export const siteConfig = {
  showReadingTime: true,
  showTags: true,
  showRelatedPosts: true,
  showLastUpdated: false,
  showAuthor: true,
}
```

### Interactive Features

```typescript
export const siteConfig = {
  commandPalette: true,
  graphView: true,
  comments: false,
  search: true,
}
```

### Layout Features

```typescript
export const siteConfig = {
  header: true,
  footer: true,
  sidebar: true,  // For documentation
  profilePicture: true,
  navigation: true,
}
```

### SEO Features

```typescript
export const siteConfig = {
  generateRSS: true,
  generateSitemap: true,
  openGraphImages: true,
  twitterCard: 'summary_large_image',
}
```

## Practical Examples

### Blog Post Example

```markdown
---
title: "Getting Started with Astro Modular"
description: "A comprehensive guide to setting up Astro Modular with Obsidian"
date: 2024-01-15
tags: ["astro", "obsidian", "blog"]
image: "posts/getting-started/cover.jpg"
imageAlt: "Astro Modular theme screenshot"
draft: false
---

# Getting Started with Astro Modular

Astro Modular transforms your Obsidian vault into a beautiful blog.

## Why Astro Modular?

> [!note] Key Feature
> Vault CMS integration means you write in Obsidian, publish automatically.

## Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/davidvkimball/astro-modular.git
cd astro-modular
npm install
```

## Configuration

Edit `src/config.ts` to set your site URL:

```typescript
siteUrl: 'https://your-blog.com'
```

## Next Steps

- [[Getting Started]] - Setup guide
- [[Theme Customization]] - Make it yours
- [[Deployment]] - Go live

%% Internal note: Remember to add more examples about wikilinks %%
```

### Page Example

```markdown
---
title: "About Me"
description: "Learn more about my background and expertise"
date: 2024-01-15
image: "pages/about/profile.jpg"
imageAlt: "My profile photo"
showTOC: false
---

# About Me

Hi, I'm a developer passionate about Obsidian and static sites.

## Background

I started using Obsidian in 2020 for personal knowledge management.

## Skills

- Astro
- TypeScript
- Obsidian
- Vault CMS

![Profile](pages/about/profile.jpg)

## Contact

You can reach me at:
- [[Contact Page|Contact me]]
- [Twitter](https://twitter.com/yourname)
```

### Project Example

```markdown
---
title: "Astro Modular Tools"
description: "A collection of utilities for Astro Modular"
categories: ["tools", "automation"]
repositoryUrl: "https://github.com/user/astro-tools"
projectUrl: "https://astro-tools.demo"
status: "completed"
featured: true
image: "projects/astro-tools/preview.png"
---

# Astro Modular Tools

A collection of scripts to enhance Astro Modular workflows.

## Features

- Image optimization
- Content validation
- Deployment automation

## Installation

```bash
npm install astro-modular-tools
```

## Usage

[View Live Demo](https://astro-tools.demo)

## Source Code

Available on [GitHub](https://github.com/user/astro-tools)

> [!tip] Related Projects
> Check out [[Another Project]] for similar tools.
```

### Documentation Example

```markdown
---
title: "Installation Guide"
category: "Getting Started"
order: 1
version: "2.0"
showTOC: true
---

# Installation Guide

Complete installation steps for Astro Modular.

## Prerequisites

Before installing, ensure you have:
- Node.js 18+
- Obsidian app
- Git

## Step 1: Clone Repository

```bash
git clone https://github.com/davidvkimball/astro-modular.git
cd astro-modular
```

## Step 2: Install Dependencies

```bash
npm install
```

## Step 3: Configure

Edit `src/config.ts` with your settings.

## Step 4: Run Development Server

```bash
npm run dev
```

Open http://localhost:4321 in your browser.

## Next Steps

- [[Configuration Guide]] - Detailed config options
- [[Theme Guide]] - Customize your theme
- [[Deployment Guide]] - Deploy to production
```

## Publishing Workflow

### Typical Workflow

1. **Write in Obsidian**:
   - Create markdown file in appropriate content folder
   - Add frontmatter with metadata
   - Use wikilinks for internal connections
   - Add images in folder with content

2. **Test Locally**:
```bash
npm run dev
# Visit http://localhost:4321
# Verify content renders correctly
```

3. **Commit Changes**:
```bash
git add .
git commit -m "Add new blog post about X"
git push
```

4. **Deploy Automatically**:
   - Netlify/Vercel: Auto-deploy on push
   - Manual: `npm run build` then upload `/dist`

### Folder Structure Example

```
my-obsidian-vault/
  content/
    posts/
      getting-started/
        index.md
        cover.jpg
      another-post.md
      another-post/
        screenshot.png
    pages/
      about/
        index.md
        profile.jpg
    projects/
      my-project/
        index.md
        preview.jpg
  src/
    config.ts  # Your theme settings
```

## Image Optimization

### Best Practices

1. **Use WebP**: Modern format, smaller files
2. **Responsive Images**: Multiple sizes for devices
3. **Descriptive Alt Text**: Accessibility and SEO
4. **Optimal Dimensions**:
   - Cover images: 1200x630px (social media)
   - Thumbnails: 600x400px
   - Inline images: 800-1200px width

### Image Frontmatter

```yaml
---
image: "posts/my-post/cover.jpg"
imageOG: true  # Use as Open Graph image
imageAlt: "Description of the image"
hideCoverImage: false  # Show cover on post page
---
```

### Lazy Loading

Images are lazy-loaded automatically. No configuration needed.

## SEO Best Practices

### Open Graph Images

Set image for social media sharing:

```yaml
---
image: "posts/my-post/og-image.jpg"
imageOG: true
imageAlt: "Compelling description for social media"
---
```

### Meta Tags

Auto-generated from frontmatter:
- `title` → `<title>` and `<og:title>`
- `description` → `<meta description>` and `<og:description>`
- `image` → `<og:image>`

### URL Structure

Clean, SEO-friendly URLs:
- Posts: `/posts/my-post-slug`
- Pages: `/about`, `/contact`
- Projects: `/projects/project-name`
- Docs: `/docs/getting-started`

### Sitemap and RSS

Auto-generated:
- Sitemap: `/sitemap-index.xml`
- RSS Feed: `/rss.xml`

## Command Palette

Press **Ctrl+K** (or **Cmd+K** on Mac) to open the command palette.

### Features

- **Fuzzy Search**: Find any page, post, or project
- **Keyboard Navigation**: Arrow keys to navigate
- **Quick Links**: Direct access to all content
- **Tag Filtering**: Search by tags

### Enable/Disable

```typescript
export const siteConfig = {
  commandPalette: true,  // Set false to disable
}
```

## Graph View

Interactive graph visualization of content connections.

### Features

- **Force-Directed Layout**: D3.js physics simulation
- **Node Types**: Different colors for posts, pages, projects
- **Interactive**: Drag nodes, zoom in/out
- **Link Detection**: Shows connections via wikilinks

### Enable/Disable

```typescript
export const siteConfig = {
  graphView: true,  // Set false to disable
}
```

## Vault CMS Integration

### Setup

1. **Install Vault CMS Plugin** in Obsidian
2. **Configure Vault Path**:
```typescript
export const siteConfig = {
  vaultPath: '/path/to/your/vault',
}
```

3. **Sync Content**:
   - Write in Obsidian
   - Files sync automatically to Astro content folder

### Benefits

- **Live Preview**: Changes reflect immediately
- **Folder Structure**: Maintains Obsidian organization
- **Asset Handling**: Images and attachments work seamlessly

## Common Patterns

### Add New Blog Post

1. Create folder: `/content/posts/my-new-post/`
2. Create file: `/content/posts/my-new-post/index.md`
3. Add frontmatter with title, date, description
4. Add images to folder
5. Test locally with `npm run dev`

### Add New Page

1. Create folder: `/content/pages/about/`
2. Create file: `/content/pages/about/index.md`
3. Add frontmatter with title, description
4. Visit `/about` after build

### Change Theme

Edit `src/config.ts`:

```typescript
export const siteConfig = {
  theme: 'tokyo-night',  // Change theme name
}
```

### Add Custom Theme

1. Create `src/themes/custom/my-theme.ts`
2. Export theme configuration
3. Set in `src/config.ts`: `theme: 'my-theme'`
4. Restart dev server

## Troubleshooting

### Images Not Showing

1. Verify image path in frontmatter
2. Run `npm run sync-images`
3. Check file exists in content folder
4. Clear browser cache

### Wikilinks Not Working

1. Wikilinks only work in **posts**, not pages
2. Verify link syntax: `[[Post Title]]` or `[[Post Title|Custom Text]]`
3. Check referenced file exists in `/content/posts/`

### Build Errors

1. Check frontmatter syntax (YAML)
2. Verify all required fields present
3. Run `npm run astro check` for diagnostics
4. Clear node_modules and reinstall

### Theme Not Applying

1. Check theme name spelling in `config.ts`
2. Restart dev server
3. Clear browser cache
4. Verify theme file exists

## References

- [Astro Modular GitHub](https://github.com/davidvkimball/astro-modular)
- [Astro Documentation](https://docs.astro.build)
- [Vault CMS](https://github.com/Glitch001/vault-cms)
- [Obsidian Help](https://help.obsidian.md)
