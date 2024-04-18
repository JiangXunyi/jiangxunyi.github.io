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

Run the `.html` on my computer

```bash
hugo server
```

## Git
Update the local repository with the remote repository
```bash
 git push --force origin master
```
### Add remote of the existing local repository
```bash
git remote add origin
```
If the exsiting remote repo is not what I want to contribute, I can change the remote repo with the following command
```bash
git remote set-url origin <url>
```
Push your code to the remote repository
```bash
git branch -M main
git push -u origin main
```


### Handle large files with git
If we want to push and track these files, we can use  `lfs` to solve this problem. First we can install `git-lfs` with the following command
```bash
brew install git-lfs
```
Then we can track the large files with the following command
```bash
git lfs track "*.psd"
# or 
git lfs track "*.pkl"
```
If you want to untrack the lsf
```bash
git lfs untrack "*.pkl"
```
After any invocation of `git-lfs-track(1)` or `git-lfs-untrack(1)`, you _must
commit changes to your `.gitattributes` file_. This can be done by running:

```bash
$ git add .gitattributes
$ git commit -m "track *.psd files using Git LFS"
```
> _Tip:_ if you have large files already in your repository's history, `git lfs
> track` will _not_ track them retroactively. To migrate existing large files
> in your history to use Git LFS, use `git lfs migrate`. For example:
>
> ```
> $ git lfs migrate import --include="*.psd" --everything
> ```
>
> **Note that this will rewrite history and change all of the Git object IDs in your
> repository, just like the export version of this command.**
>

If some are extremely big and I don't want to track them, I can use the following command. For instance, I want to ignore these two file: data/dbpedia/kg.pkl
data/dbpedia/mappingbased-objects_lang=en.ttl
- add the filename into the `.gitignore` file
- add `.gitignore` file into the git repo 
```bash
git add .gitignore
```
- commit the changes
```bash
git commit -m "add .gitignore file"
```
- push the changes to the remote repo
```bash
git push origin main
```

But I encounter with the problem that the large files have been tracked by git, I can use the following command to clean the history of the git repo
```bash
git filter-branch --index-filter 'git rm --cached --ignore-unmatch data/dbpedia/kg.pkl' --prune-empty -- --all
```

### Uninstall lfs
Cause my files are too large, so I just ignore the files in the `dataset` folder. But I have already installed `lfs` in my computer. I can uninstall it with the following command
```bash
git lfs uninstall
```

After uninstall, I need to clear the cache with the following command
```bash
git rm -r --cached .
```
Since in the `.gitignore` file, we already ignore the dataset folder.
Use 
```bash
git add .
```

However, I still have the large files in the git commit history, so I just remove `.git` and init a new git repo
```bash
rm -rf .git
git init
```

Finally, I ignore the large files in the original repo and push my code to the remote repo. (Actually during this process, I encouter with the secret leak error and I need to modify my code with personal information)


## HCP
This part is the useful command lines for HCP, mainly refer to this [tutorial](https://help.nscc.sg/wp-content/uploads/Workshop-Handbook_ASPIRE2A-Mar2023.pdf)

### 1. Connect to HCP
I use vscode to connect to HCP, which need NUS web VPN. 

### 2. Create Conda Environment
Before I run the code, I need to create a conda environment. The official website of [miniconda](https://docs.anaconda.com/free/miniconda/miniconda-install.html)

```bash
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
``` 
After installing
```bash
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh
```

Create a new environment
```bash 
conda create -n myenv python=3.10
```

Activate the environment
```bash
conda activate myenv
```

### 3. Bash Script for job submission
```bash
#!/bin/bash
#PBS -N LLaMA2_FineTuning
#PBS -l select=8:ncpus=128:mem=440G:mpiprocs=128:ompthreads=1
#PBS -l walltime=3:00:00
#PBS -j oe
#PBS -o fine-tuning-output.txt
#PBS -P xunyi
#PBS -q ai

# 加载Anaconda环境
echo "Python interpreter: $(which python)"
module load cray-python/3.9.7.1
# source activate /home/users/nus/e1325135/miniconda3/envs/llms
source ~/miniconda3/etc/profile.d/conda.sh
conda activate llms
echo $CONDA_DEFAULT_ENV


# 进入你的工作目录（如果有的话）
cd scratch/llama2_inspire

# 执行fine-tuning脚本，这里假设是一个Python脚本
# 你需要根据你的具体情况修改脚本名称和路径，以及传递给它的参数
# python fine_tune_llama2.py 

# 修改为直接指定解释器路径
/home/users/nus/e1325135/miniconda3/envs/llms/bin/python fine_tune_llama2.py
```

### 4. Submit the job and job status
```bash
qsub fine_tuning.sh
qstat
```

## tmux command lines
- Create a new tumx session
  ```bash
  tmux new -s <session-name>
  ```

- Look up the existed sessions
  ```bash
  tmux list-session
  ```

- Detach the session
Using `exit` or `ctrl + b d` to exit

- Attach the session
  ```bash
  tmux attach -t <session-id>
  tmux attach -t <session-name>
  ```

  



