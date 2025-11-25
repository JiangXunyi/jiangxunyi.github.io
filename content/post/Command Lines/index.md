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
  - Open Source

categories:
  - Study Notes

enable_math: True
---


# The Useful Command Lines 
**Xunyi Jiang**
## Permanently Add to PATH

To permanently add `conda` to your `PATH`, you need to add the above `export` command to your shell configuration file, such as `.bashrc` or `.bash_profile` (depending on the shell and operating system you use).

1. Open your shell configuration file. If you're using bash, it's usually `.bashrc` or `.bash_profile`:

   ```bash
   nano ~/.bashrc
   ```

2. Add the following line at the end of the file:

   ```bash
   export PATH=~/miniconda3/bin:$PATH
   ```

3. Save and close the file. (If you're using nano, you can press `Ctrl + O` to save, then press `Ctrl + X` to exit.)

4. To make the changes take effect, you need to reload the configuration file, which can be done by running the following command or by closing and reopening your terminal:

   ```bash
   source ~/.bashrc
   ```


## Website

Run the `.html` on my computer

```bash
hugo server
```

## Git
Some useful command lines for git(You'd better remember it)
```bash
git clone <repo_url> # clone
git add . # add file to track
git commit -m "This is the comment for this commit" # commit the change
git push origin main # push to remote
git push origin feature-branch # push to the certain branch
git branch -b new_branch_name # create a new branch and check to this branch
git checkout brach_name
git branch new_branch_name # creat a new branch without checkout.
git pull origin <branch_name> # pull the revision of branch
git log -p -1 # check the last commit 
# after check, how to quit in ternimal? q
git add remote <ssh>
git checkout -b <branch_name> # checkout and new a branch
git merge <branch_name> # if we want to merge 2 branch, we need to first check to the branch we want to mergem then use this command line to merge
```


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

# Load Anaconda environment
echo "Python interpreter: $(which python)"
module load cray-python/3.9.7.1
# source activate /home/users/nus/e1325135/miniconda3/envs/llms
source ~/miniconda3/etc/profile.d/conda.sh
conda activate llms
echo $CONDA_DEFAULT_ENV


# Enter your working directory (if applicable)
cd scratch/llama2_inspire

# Execute fine-tuning script, assuming it's a Python script here
# You need to modify the script name and path according to your specific situation, as well as the parameters passed to it
# python fine_tune_llama2.py 

# Modified to directly specify interpreter path
/home/users/nus/e1325135/miniconda3/envs/llms/bin/python fine_tune_llama2.py
```

### 4. Submit the job and job status
```bash
qsub fine_tuning.sh
qstat
```
As for slurm job, we can use the following command
```bash
squeue -u $USER
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

## Download file from remote server
```bash
ssh e1325135@aspire2a.nus.edu.sg
Download file: scp e1325135@aspire2a.nus.edu.sg:~/scratch/scripts/ProjectCode/DatabaseCreationCodes/DatabaseCreation.ipynb /Users/xunyijiang/Documents/StudyMaterials/2024Spring/CRS/explainableCRS/ProjectCode/DatabaseCreationCodes/DatabaseCreationCodeFullVersion.ipynb

scp e1325135@aspire2a.nus.edu.sg:~/scratch/scripts/ProjectCode/dataset/restuls/data0416/my_info_v3.csv /Users/xunyijiang/Documents/StudyMaterials/2024Spring/CRS/explainableCRS/ProjectCode/dataset/results/data0416/movie_db.csv
```

## Check GPU Thread Usage
```bash
fuser -v /dev/nvidia* 
```
## Batch Delete Processes on GPU 4
```bash
fuser -v /dev/nvidia4 |awk '{for(i=1;i<=NF;i++)print "kill -9 " $i;}' |  sh
```

## Remote SSH
1. Why I need SSH?
- Higher security: SSH uses encrypted key pairs (private key and public key) for authentication instead of username and password. This makes your operations more secure, especially on public networks.
- Password-free login: Once you set up SSH keys and add the public key to GitHub, you don't need to enter username and password for every operation. This greatly simplifies operations.
- Avoid HTTP restrictions: In some network environments, HTTP may be restricted or encounter HTTP2 framing layer problems as you've seen before. SSH is usually not subject to these restrictions.

2. How to set
- First we need to generate ssh key:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com" # jiangxy2020@mail.sustech.edu.cn
# then it will store the generated key into  `~/.ssh/id_ed25519`
cat ~/.ssh/id_ed25519.pub # get the generated public key
```

After finish all this set on my own laptop, I need to set up at GitHub.
Settings > SSH > Add new key.
I use this method to solve the problem of unsuccessful push.



## Sync Remote Folders
```bash
rsync -avz --delete /path/to/local/project/ ubuntu@ec2-35-94-87-47.us-west-2.compute.amazonaws.com:pa1
```
rsync -avz --delete /Users/xunyijiang/Documents/AStudyUCSD/2024Fall/CSE260/PAs/PA1/pa1-faz007-xuj003/ ubuntu@172.31.54.108:~/pa1


## Check brew Path
```bash
brew info openblas
```

  



