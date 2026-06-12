---
layout: distill
title: Research Article Template
description: A template for writing research-style blog posts with math, citations, interactive diagrams, and sidenotes. Copy this file to start a new post.
tags: template
categories: tutorial
date: 2024-01-01
featured: false
published: false

authors:
  - name: Jayanth S
    url: "https://js2498.github.io"
    affiliations:
      name: TCS Research

bibliography: 2024-01-01-research-article-template.bib

toc:
  - name: Writing Math
  - name: Citations and Footnotes
  - name: Figures and Diagrams
  - name: Code Blocks
  - name: Sidenotes and Asides
---

## Writing Math

Inline math works with single dollar signs: $$E = mc^2$$.

Display math uses double dollar signs or `\[ ... \]`:

$$
\mathcal{L}(\theta) = \mathbb{E}_{\tau \sim \pi_\theta}\left[\sum_{t=0}^{T} \gamma^t r(s_t, a_t)\right]
$$

For aligned multi-line equations:

$$
\begin{align}
  \delta_t &= r_t + \gamma V(s_{t+1}) - V(s_t) \\
  V(s) &\leftarrow V(s) + \alpha \delta_t
\end{align}
$$

---

## Citations and Footnotes

You can cite papers from the `.bib` file in the same directory as this post.
For example: <d-cite key="example2024"></d-cite>.

Footnotes use the `<d-footnote>` tag. <d-footnote>This is a footnote. It appears in the margin on wide screens and inline on mobile.</d-footnote>

---

## Figures and Diagrams

A basic figure with a caption:

<figure>
  <img src="/assets/img/prof_pic.jpg" alt="An example figure" style="max-width: 300px;">
  <figcaption>Fig. 1 — An example figure caption.</figcaption>
</figure>

For interactive plots, you can use D3.js. Embed the script directly or reference an external JS file.

---

## Code Blocks

Python with syntax highlighting:

```python
import numpy as np

def bellman_update(V, R, P, gamma=0.99):
    """Single Bellman backup."""
    return R + gamma * P @ V
```

Inline code: `bundle exec jekyll serve`.

---

## Sidenotes and Asides

Use `<d-aside>` for margin notes visible on wide screens:

<d-aside>
This is a sidenote. Use it for supplementary material that doesn't break the main flow.
</d-aside>

Main text continues here. Sidenotes appear in the margin on desktop and inline on mobile.

---

## Tips for New Posts

1. **Copy this file** and rename it `YYYY-MM-DD-your-title.md`.
2. **Create a matching `.bib` file** at `_bibliography/YYYY-MM-DD-your-title.bib` for per-post references.
3. Set `published: true` when ready to go live.
4. Set `featured: true` to pin it to the top of the blog index.
5. Use `layout: post` instead of `layout: distill` for shorter, less structured posts.
