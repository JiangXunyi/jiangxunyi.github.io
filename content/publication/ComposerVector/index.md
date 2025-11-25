---
title: "Composer Vector: Style-steering Symbolic
Music Generation in a Latent Space"
authors:
- admin
- Julian McAuley
- Xin Xu*
date: "2025-11-24T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2025-11-24T00:00:00Z"

# Publication type.
# Accepts a single type but formatted as a YAML list (for Hugo requirements).
# Enter a publication type from the CSL standard.
publication_types: ["article"]

# Publication name and optional abbreviated publication name.
publication: ""
publication_short: ""

abstract: Symbolic music generation has made significant progress, yet achieving finegrained and flexible control over composer style remains challenging. Existing training-based methods for composer style conditioning depend on large labeled datasets. Besides, these methods typically support only single-composer generation at a time, limiting their applicability to more creative or blended scenarios. In this work, we propose Composer Vector, an inference-time steering method that operates directly in the model’s latent space to control composer style without retraining. Through experiments on multiple symbolic music generation models, we show that Composer Vector effectively guides generations toward target composer styles, enabling smooth and interpretable control through a continuous steering coefficient. It also enables seamless fusion of multiple styles within a unified latent-space framework. Overall, our work demonstrates that simple latent-space steering provides a practical and general mechanism for controllable symbolic music generation, enabling more flexible and interactive creative workflows.

tags:
- Machine Learning
- Deep Learning
- NLP
featured: false

links:
- name: demo
  url: https://jiangxunyi.github.io/composervector.github.io/
url_pdf: https://openreview.net/pdf/d01d8065fcb950efd6bd5c50197b1b5084e7ce50.pdf
url_code: 'https://github.com/JiangXunyi/Composer-Vector'
# url_dataset: '#'
# url_poster: '#'
# url_project: ''
# url_slides: ''
# url_source: '#'
# url_video: '#'

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: 'Image credit: [**Your Source**](featured.jpg)'
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

<!-- Add any additional content, notes, or rich formatting here -->