# Academic Project Template

A comprehensive template for academic papers and presentations at Hochschule der Medien Stuttgart. Includes automated workflows for building Typst papers and deploying Slidev presentations to GitHub Pages.

## Features

- **Typst Paper Template**: HdM-styled academic paper with customizable parameters
- **Slidev Presentation**: Modern glass-themed presentation template
- **GitHub Actions**: Automated building and deployment
- **Toggleable Workflows**: Enable/disable paper or presentation workflows via config
- **Professional Styling**: Pre-configured HdM formatting and glassmorphism theme

## Quick Start

### 1. Use This Template

Click "Use this template" on GitHub or clone this repository:

```bash
git clone https://github.com/yourusername/academic-project-template.git my-project
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

Edit `presentation/slides.md`:

```markdown
---
title: Your Presentation Title
---

# Your Title

Content here...
```

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
npm run dev
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
1. Builds Slidev presentation
2. Deploys to GitHub Pages
3. Accessible at `https://username.github.io/repo-name/slides/`

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

The presentation uses a custom "Liquid Glass Dark Theme" with glassmorphism effects.

**Available classes:**
- `.glass-card`: Glassmorphic card with hover effects
- `.glass-panel`: Larger glassmorphic panel
- `.subtitle`: Subtitle styling

**Modify theme:** Edit `presentation/style.css`

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
│   ├── style.css                 # Glass theme styles
│   └── package.json              # Slidev dependencies
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

### Presentation Modes

Slidev supports multiple views:
- **Slides:** `/slides/`
- **Presenter:** `/slides/presenter`
- **Overview:** `/slides/overview`

## License

MIT License - feel free to use and modify for your academic projects.

## Credits

- Template styling based on HdM academic standards
- Glass theme inspired by modern UI design trends
- Built with [Typst](https://typst.app/) and [Slidev](https://sli.dev/)
