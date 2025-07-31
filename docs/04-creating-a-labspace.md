# 🔨 Creating a Labspace

Now that you've got an idea of what a Labspace _is_, it's important to take a moment and talk about how to make a Labspace.

## 📦 The content repository

The content repository is a publicly accessible repo that provides everything for the Labspace - docs, sample app files, etc.

### The `labspace.yaml` file

The `labspace.yaml` file defines the configuration for the Labspace. It **must be at the root of the repo.**

The file consists of the following items:

```yaml
title: The Labspace title
description: >
  The subtitle or description of the Labspace

sections:
  - title: Section One
    contentPath: ./path/to/section-one.md
  - title: Section Two
    contentPath: ./section-two.md
  - title: Section Three
    contentPath: ./docs/section-three.md
```

Each "section" is a different tab/step in the Labspace and can use a Markdown file located anywhere in the repository.

