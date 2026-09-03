---
title: "Toward Latent Language Model Skills Steering and Optimization: An Empirical Study"
authors:
- admin
- Junda Wu
- Yuxin Xiong
- Sheldon Yu
- Tong Yu
- David Arbour
- Ritwik Sinha
- Julian McAuley
- Hongyi Wen*
date: "2026-09-03T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2026-08-29T00:00:00Z"

# Publication type.
# Accepts a single type but formatted as a YAML list (for Hugo requirements).
# Enter a publication type from the CSL standard.
publication_types: ["article"]

# Publication name and optional abbreviated publication name.
publication: "Accepted by EMNLP 2026"
publication_short: "EMNLP Main"

abstract: >-
  Skills, as a useful abstraction for the procedural capabilities of large language models (LLMs), capture how models perform structured, multi-step reasoning and program execution. Existing approaches typically treat skills as explicit, surface-level constructs specified through prompts or programs, leaving open the question of how such procedural capabilities are represented inside the model and whether they can be manipulated as structured objects in latent space. In this empirical study, we investigate whether procedural LLM skills can be represented as directions in activation space and whether vector-space operations over these directions can express skill-level behaviors. We find that procedural skills admit a vector-space representation: individual skill directions can be activated to shift model behavior; independently extracted directions can compose to form higher-level skills. Contrastive directions yield context-conditioned algorithmic personalization and optimization trajectories over skill directions evolve non-monotonically, with intermediate states often surpassing fully optimized solutions. These results support a representation-level view of procedural LLM skills， they admit a latent vector-space organization that allows direct manipulation through internal interventions.

tags:
- Source Themes
featured: false

links:
# - name: Custom Link
#   url: http://example.org
url_pdf: https://arxiv.org/html/2608.29459v1
# url_code: 'https://github.com/JiangXunyi/BenchAge'
# url_dataset: '#'
# url_poster: '#'
# url_project: ''
# url_slides: ''
# url_source: '#'
# url_video: '#'

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: 'Image credit: [**Unsplash**](problem_formulation.png)'
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects:
- internal-project

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: example
---

<!-- {{% callout note %}}
Create your slides in Markdown - click the *Slides* button to check out the example.
{{% /callout %}} -->

<!-- Add the publication's **full text** or **supplementary notes** here. You can use rich formatting such as including [code, math, and images](https://docs.hugoblox.com/content/writing-markdown-latex/). -->
