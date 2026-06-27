# Academic Project Template

A comprehensive template for academic papers and presentations at Hochschule der Medien Stuttgart. Includes automated workflows for building Typst papers and deploying Marp presentations to GitHub Pages.

## Features

- **Typst Paper Template**: HdM-styled academic paper with customizable parameters
- **Marp Presentation**: Markdown-based slide deck using a built-in Marp theme
- **GitHub Actions**: Automated building and deployment
- **Toggleable Workflows**: Enable/disable paper or presentation workflows via config
- **Professional Styling**: Pre-configured HdM paper formatting

## Quick Start

### 1. Use This Template

Click "Use this template" on GitHub or clone this repository:

```bash
git clone https://github.com/julian-schn/academic-project-template.git my-project
cd my-project
```

### 2. Configure Features

Edit `config.yml` to enable/disable paper or presentation:

```yaml
features:
  paper: true           # Set to false to disable paper workflow
  presentation: true    # Set to false to disable presentation workflow
```

### 3. Paper Setup

Edit `paper/paper.typ`:

```typst
#import "lib.typ": academic-paper

#show: academic-paper.with(
  title: "Your Paper Title",
  author: "Your Name",
  email: "your.email@hdm-stuttgart.de",
  course: "Course Name (123456)",
  instructor: "Instructor Name",
  semester: "Wintersemester 2025/2026",
  abstract: [Your abstract here],
  bibliography-file: "references.bib",
)

= Introduction
Your content here...
```

Add references to `paper/references.bib`.

### 4. Presentation Setup

Edit `presentation/slides.md`. Slides are plain Markdown separated by `---`:

```markdown
---
marp: true
theme: gaia
class: invert
paginate: true
title: Your Presentation Title
---

<!-- _class: lead -->

# Your Title

Content here...

---

# Next Slide

- Point 1
- Point 2
```

Swap `theme:` for any built-in Marp theme (`default`, `gaia`, `uncover`) and remove `class: invert` for a light look.

### 5. Local Development

**Paper:**
```bash
# Install Typst: https://github.com/typst/typst
typst watch paper/paper.typ
```

**Presentation:**
```bash
cd presentation
npm install
npm run dev      # live preview server with watch
npm run build    # build static HTML -> dist/index.html
npm run export   # export to PDF -> dist/slides.pdf (requires Chrome/Chromium)
```

## GitHub Actions

### Paper Workflow

**Triggers:**
- Push to `main` branch (changes in `paper/**`)
- Manual trigger via workflow_dispatch

**What it does:**
1. Builds Typst PDF
2. Commits timestamped PDF to root (`paper-YYYY-MM-DD-HHMM.pdf`)
3. Creates artifact for download
4. On tags: Creates release with PDF

**Disable:** Set `features.paper: false` in `config.yml`

### Presentation Workflow

**Triggers:**
- Push to `main` branch (changes in `presentation/**`)
- Manual trigger via workflow_dispatch

**What it does:**
1. Builds the Marp presentation to a single self-contained HTML file
2. Deploys to GitHub Pages
3. Accessible at `https://username.github.io/repo-name/`

**Disable:** Set `features.presentation: false` in `config.yml`

**Setup GitHub Pages:**
1. Go to repo Settings → Pages
2. Set Source to "GitHub Actions"

## Template Customization

### Paper Template Parameters

```typst
#show: academic-paper.with(
  title: "",              // Paper title
  author: "",             // Author name
  email: "",              // Email address
  institution: "",        // University name
  faculty: "",            // Faculty name
  program: "",            // Degree program
  course: "",             // Course name and ID
  instructor: "",         // Instructor name
  semester: "",           // Semester
  date: datetime.today(), // Date

  paper-size: "a4",       // Paper size
  font: "New Computer Modern",  // Font
  font-size: 11pt,        // Font size
  line-spacing: 1.5,      // Line spacing

  abstract: none,         // Abstract content
  acknowledgments: none,  // Acknowledgments
  bibliography-file: none, // BibTeX file
)
```

### Presentation Theme

The presentation uses a built-in Marp theme, set via the `theme:` key in the
`slides.md` front-matter. Available built-in themes: `default`, `gaia`, `uncover`.
The template defaults to `gaia` with `class: invert` for a dark look.

**Useful per-slide directives** (written as HTML comments):
- `<!-- _class: lead -->`: large, centered title slide
- `<!-- _paginate: false -->`: hide the page number on a slide
- `<!-- _backgroundColor: #123 -->`: override the background for one slide

**Marp CLI settings** (e.g. enabling raw HTML) live in `presentation/marp.config.js`.

## Project Structure

```
academic-project-template/
├── .github/
│   └── workflows/
│       ├── build-paper.yml       # Paper build workflow (conditional)
│       └── deploy-slides.yml     # Presentation deploy workflow (conditional)
├── paper/
│   ├── lib.typ                   # Reusable paper template
│   ├── paper.typ                 # Your paper content
│   └── references.bib            # Bibliography
├── presentation/
│   ├── slides.md                 # Presentation content
│   ├── marp.config.js            # Marp CLI settings
│   └── package.json              # Marp dependencies
├── config.yml                    # Toggle workflows
├── .gitignore
├── typst.toml                    # Typst package metadata
└── README.md
```

## Tips

### Creating a Release

To trigger a GitHub release with the PDF:

```bash
git tag v1.0
git push origin v1.0
```

This creates a release and attaches the PDF.

### Multiple Papers

For multiple papers, create subdirectories:

```
paper/
├── lib.typ
├── paper1/
│   ├── paper.typ
│   └── references.bib
└── paper2/
    ├── paper.typ
    └── references.bib
```

Update workflow paths accordingly.

## License

MIT License - feel free to use and modify for your academic projects.

## Credits

- Template styling based on HdM academic standards
- Built with [Typst](https://typst.app/) and [Marp](https://marp.app/)
