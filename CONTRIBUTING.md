# Contributing

Thanks for your interest in contributing to the Style Guide.

## How to Contribute

1. **Fork** the repository
2. **Create a branch** for your changes (`git checkout -b add-toast-pattern`)
3. **Follow the existing structure** — each document uses consistent heading hierarchy and code snippet formatting
4. **Submit a pull request** with a clear description of what you added or changed

## Document Structure

### Site Deep-Dives (`sites/`)

Each site document follows this template:

1. Identity & Mood (1 paragraph)
2. Color Palette (table with hex, swatch, usage)
3. Typography
4. Spacing & Layout
5. Component Catalog (with code snippets)
6. Animation & Motion
7. Responsive Design
8. How to Adapt This Style

### Pattern Documents (`patterns/`)

Each pattern document includes:

1. Overview of the pattern
2. Variants from each site (with annotated code)
3. Visual description
4. How to Apply This Pattern (with alternative project examples)

### Foundation Documents (`foundations/`)

Cross-site comparison tables showing how each site handles the same design token differently.

### Guide Documents (`guides/`)

Step-by-step instructions with concrete examples for applying an aesthetic to a new project.

## Code Snippets

- Use fenced code blocks with language tags (`css`, `jsx`, `html`)
- Annotate with comments explaining *why*, not just *what*
- Keep snippets focused — show the relevant pattern, not entire files
- Use HTML color swatches for color references: `<img src="https://via.placeholder.com/12/hex/hex.png" width="12" height="12" />`

## Style

- Write in present tense
- Be specific — include exact values (hex codes, pixel sizes, easing functions)
- Link between documents using relative paths
- Every "How to Apply" section should include at least 2 concrete alternative project examples
