---
title: The Useful Command Lines
subtitle: 

# Summary for listings and search engines
summary: 

# Link this post with a project
projects: []

# Date published
date: '2023-12-25T00:00:00Z'

# Date updated
lastmod: '2023-12-25T00:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
# image:
#   caption: 'Image credit: [**Unsplash**]()'
#   focal_point: ''
#   placement: 2
#   preview_only: false

authors:
  - admin
  - Xunyi Jiang

tags:
  - Academic
  - 开源

categories:
  - Study Notes

enable_math: True
---


# The Useful Command Lines 
**Xunyi Jiang**
## 永久添加到 PATH

为了永久添加 `conda` 到你的 `PATH`，你需要将上述 `export` 命令添加到你的 shell 配置文件中，如 `.bashrc` 或 `.bash_profile`（取决于你使用的 shell 和操作系统）。

1. 打开你的 shell 配置文件。如果你使用的是 bash，通常是 `.bashrc` 或 `.bash_profile`：

   ```bash
   nano ~/.bashrc
   ```

2. 在文件的末尾添加以下行：

   ```bash
   export PATH=~/miniconda3/bin:$PATH
   ```

3. 保存并关闭文件。（如果你使用的是 nano，可以按 `Ctrl + O` 保存，然后按 `Ctrl + X` 退出。）

4. 为了使更改生效，你需要重新加载配置文件，可以通过运行以下命令或者关闭并重新打开你的终端：

   ```bash
   source ~/.bashrc
   ```


## Website