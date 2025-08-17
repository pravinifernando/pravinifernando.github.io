# Fernando Research Group Website

A Jekyll-based academic website for the Fernando Research Group at Union College.

## Making Changes to the Website

### 1. Preview Changes Locally

Before publishing changes, see them on your computer first:

```bash
jekyll serve
```

This creates a local preview at `http://localhost:4000`. The site updates automatically when you save files.

### 2. Build the Website

After making changes, build the final website:

```bash
jekyll build
```

This creates the files that will be published online.

### 3. Publish Changes to GitHub

Save your changes to GitHub so they appear online:

```bash
git add .
git commit -m "Update website content"
git push
```

Replace "Update website content" with a brief description of what you changed.

## Adding Photos to Gallery

Edit `gallery.md` and add new photos to the `galleryPhotos` array:

```javascript
{
    src: "assets/img/your-photo.jpg",
    alt: "Description of photo",
    date: "Month Year", 
    caption: "Photo caption",
    isGroupPhoto: true  // true = shows in carousel, false = grid only
}
```

## Common Tasks

- **Edit content**: Modify `.md` files (index.md, about.md, etc.)
- **Add team members**: Edit `team.md` 
- **Update publications**: Edit `publications.md`
- **Add navigation links**: Edit `_data/nav.yml`