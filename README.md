# Sagging Royalties Documentation

This repository contains the source code for the official documentation site of the **Sagging Royalties** ecosystem (Facecards). It is built using [MkDocs](https://www.mkdocs.org/) and the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

## 🚀 Getting Started

### Prerequisites

-   **Python 3.13+**
-   **[uv](https://github.com/astral-sh/uv)** (recommended package manager)

### Installation

1.  Clone the repository (if you haven't already):
    ```bash
    git clone ...
    cd saggingroyals-docs
    ```

2.  Install dependencies:
    ```bash
    uv sync
    ```

## 🛠 Usage

### Live Development

Start the local development server. This will automatically reload the site when you make changes to markdown files.

```bash
uv run mkdocs serve
```

Open your browser to [http://127.0.0.1:8000](http://127.0.0.1:8000).

### Building for Production

To build the static site (output to `site/`):

```bash
uv run mkdocs build
```

## 📂 Project Structure

-   `mkdocs.yml`: Main configuration file (nav structure, theme settings).
-   `docs/`: Contains all markdown source files and assets.
    -   `index.md`: The homepage.
    -   `assets/`: Images and other static files.
-   `site/`: The generated static site (ignored by git).

## 📚 Resources & Documentation

-   **MkDocs**: [User Guide](https://www.mkdocs.org/user-guide/writing-your-docs/)
-   **Material for MkDocs**: [Reference](https://squidfunk.github.io/mkdocs-material/reference/)
    -   [Admonitions](https://squidfunk.github.io/mkdocs-material/reference/admonitions/) (Callouts/Notes)
    -   [Code Blocks](https://squidfunk.github.io/mkdocs-material/reference/code-blocks/)
    -   [Icons & Emojis](https://squidfunk.github.io/mkdocs-material/reference/icons-emojis/)
