---
name: write-blog
description: Write and publish blog posts in the SvelteKit markdown blog with header images, proper frontmatter, and organized media files.
---

## What I do

I guide you through creating and publishing visually-rich blog posts in this SvelteKit markdown blog. I ensure proper file structure, header images, frontmatter format, image handling, and markdown syntax.

![Blog Writing Flow](/blog-images/GettingStarted/config-file.png)

## When to use me

Use this skill whenever you need to:

- Create a new blog post with header image
- Add a blog to the static/blogs/ directory
- Publish content with proper metadata and visuals
- Organize blog images in the correct folder structure
- Enhance posts with images, diagrams, and visual content

## Blog Post Format

### File Location

```
static/
├── blogs/                    # Blog markdown files
│   ├── getting-started.md
│   └── my-first-blog.md
└── blog-images/              # Blog media files
    ├── GettingStarted/
    │   ├── config-file.png
    │   └── header.png
    └── MyFirstBlog/
        ├── header.png
        ├── setup.png
        └── diagrams/
            └── workflow.svg
```

- Blog markdown files go in: `static/blogs/`
- Blog images go in: `static/blog-images/<BlogName>/`
- Use kebab-case for filenames: `my-first-blog.md`

### Frontmatter (Required Metadata)

Every blog post must start with YAML frontmatter with a header image:

```yaml
---
title: Your Blog Title Here
date: 2025-01-15
category: 'Category Name'
description: 'A short description for SEO and blog previews'
header: /blog-images/<BlogName>/header.png
---
```

**Frontmatter fields:**

- `title` (required): The blog post title
- `date` (required): Publication date in YYYY-MM-DD format
- `category` (required): Category in quotes (e.g., "Guides", "Journal", "Tech")
- `description` (required): Brief description for SEO and blog previews
- `header` (recommended): Path to header image for the blog card

### Content Structure

Write your content below the frontmatter using Markdown syntax. Use images to enhance readability.

## Image Handling

### Creating Image Folders

```
static/blog-images/
└── <BlogName>/
    ├── header.png            # Required: Header image for blog card
    ├── photo.jpg             # Optional: Inline images
    └── diagrams/             # Optional: Diagrams and charts
        └── architecture.svg
```

1. Create folder: `static/blog-images/<BlogName>/`
2. Add a `header.png` for the blog card preview
3. Place all images for the blog in this folder
4. Reference images using absolute paths from static

### Image Syntax

```markdown
![Image Title](/blog-images/MyBlog/header.png)
![Photo](/blog-images/MyBlog/photo.jpg)
![Diagram](/blog-images/MyBlog/diagrams/architecture.svg)
```

### Header Image Best Practices

- **Recommended size**: 1200x630px (like Open Graph images)
- **Format**: PNG or JPG for photos, SVG for diagrams
- **Purpose**: Displayed on blog listing cards and social media previews

## Visual Examples

### Folder Structure Diagram

![Folder Structure](/blog-images/GettingStarted/config-file.png)

### Blog Card Preview

```
┌─────────────────────────────────────────────────────┐
│  [Header Image: 1200x630px]                         │
│                                                     │
│  Title: Getting Started                             │
│  Date: 2025-11-06 | Category: Guides               │
│                                                     │
│  Description: Quick start guide to configure...     │
└─────────────────────────────────────────────────────┘
```

## Supported Markdown Syntax

### Headings

```markdown
# Heading 1

## Heading 2

### Heading 3
```

### Text Formatting

```markdown
**Bold text**
_Italic text_
~~Strikethrough~~
`inline code`
```

### Images

```markdown
![Setup Guide](/blog-images/MyFirstBlog/setup.png)
![Architecture Diagram](/blog-images/MyFirstBlog/diagrams/architecture.svg)
```

### Links

```markdown
[Link Text](https://example.com)
```

### Lists

```markdown
- Unordered item 1
- Unordered item 2

1. Ordered item 1
2. Ordered item 2
```

### Code Blocks

```javascript
console.log('Hello World');
// Syntax highlighting is automatic
```

### Blockquotes

```markdown
> This is a blockquote
> Multiple lines work too
```

### Tables

```markdown
| Header 1 | Header 2 |
| -------- | -------- |
| Cell 1   | Cell 2   |
```

### Math (KaTeX)

This blog supports LaTeX math rendering:

```markdown
Inline: $E = mc^2$

Block:

$$
\sum_{i=1}^n i^2 = \frac{n(n+1)(2n+1)}{6}
$$
```

## Example Blog Post with Header Image

````yaml
---
title: My First Blog Post
date: 2025-01-15
category: "Guides"
description: "A comprehensive guide on how to write and publish blog posts in this project"
header: /blog-images/MyFirstBlog/header.png
---

![Blog Setup](/blog-images/MyFirstBlog/setup.png)

## Introduction

Welcome to my new blog! This is an example of how to write visually-rich posts with header images and inline screenshots.

## Getting Started

Here's how you get started with step-by-step visuals:

![Step 1: Fork](/blog-images/MyFirstBlog/step1-fork.png)

1. Fork the repository
2. Clone it locally
3. Run `pnpm dev`

![Development Server](/blog-images/MyFirstBlog/dev-server.png)

## Code Example

```typescript
function greet(name: string): string {
  return `Hello, ${name}!`;
}
```

## Architecture

![Architecture Diagram](/blog-images/MyFirstBlog/diagrams/architecture.svg)

## Conclusion

That's it! Happy writing with images.

````

## Step-by-Step Process

1. **Determine the blog name**: Use kebab-case (e.g., `my-first-post`)
2. **Create the image folder**: `static/blog-images/<BlogName>/`
3. **Add a header image**: Create `header.png` (1200x630px recommended)
4. **Create the markdown file**: `static/blogs/<BlogName>.md`
5. **Add frontmatter**: Include title, date, category, description, and header path
6. **Write content**: Use Markdown syntax with images to enhance readability
7. **Add supporting images**: Place in image folder and reference with `/blog-images/...`
8. **Save and verify**: The blog will automatically appear in the feed with the header image

## Categories

Common categories used in this blog:

- Guides
- Journal
- Tech
- Tutorial
- Notes

Use an existing category or create a new one as needed.

## Verification

After creating a blog post:

- The header image appears on the blog listing card
- Posts are sorted by date (newest first)
- The description appears in blog previews
- All images load correctly from the static folder
- Social media previews show the header image

```

```
