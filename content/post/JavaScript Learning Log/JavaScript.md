---
title: My JavaScript Learning Log
subtitle: 

# Summary for listings and search engines
summary: 

# Link this post with a project
projects: []

# Date published
date: '2024-08-11T00:00:00Z'

# Date updated
lastmod: '2024-08-11T00:00:00Z'

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
# Node.js Basic Knowledge
## Node.js
Node.js is a free, open-source, cross-platform JavaScrip runtime evnvironment that lets developers to create servers, web apps, command line tools and scrips.
I ananogy this with python interpreter, or Java interpreter.

## npm: node package management
This note is mainly based on <a href="[hyperlink address](https://www.freecodecamp.org/chinese/news/what-is-npm-a-node-package-manager-tutorial-for-beginners/)" title="This blog: What is npm - A guide for beginners">This blog: What is npm - A guide for beginners</a>
npm is the default package manager for the JavaScript runtime Node.js, mainly composed of two parts:
- A CLI (Command Line Interface) tool for publishing and downloading packages
- An online repository for hosting JavaScript packages
Think of npm as a system that helps you install, update, and manage libraries (packages) that your project depends on. These packages might provide various functionalities, like working with dates, making HTTP requests, or even running a web server.

## package.json
This file acts as the blueprint for your project. It contains information about your project (like its name, version, and description) and lists the packages your project depends on. When you share your project, others can use npm to quickly install all the required packages based on what's in the package.json file.

To use a metaphor: Imagine you're sending a package via mail. The package has a label with information about where it's going, who sent it, and what's inside. Similarly, package.json is like that label for your project. It tells npm (and other developers) what your project is, what it needs, and how it should be handled.


# Environment setup
Just like python, there are lots of different versions of `Node.js`. I need a tool to manage my node version.
Here are some tools: n/nvm. I use n to manage it. But I encounter with trenmendous problems. Here I will list them and how I solved them.
## Install n
Because there is node.js on my laptop, so I have npm as well.
```bash
npm install -g n # use npm 
brew install n # or use brew
```
After installed n, I can use n to install different version of node.js. 
```bash
# install v16.15.0
n 16.15.0
```
After install this version, I can choose which version to use
```bash
n use 16.15.0 # shift version
node -v # check the version
```
Here comes the problem: I cannot change the version. `node -v` still shows that I was in v20.6.0
In this way, I chech the path of node.js
```bash
which node
```
I found that the path is `/opt/homebrew/bin/node`, but the path of n is `/urs/local/`. So I need to change the path of node.js to the path of n. Or I need to install node.js into the same directory.
```bash
nano ~/.zshrc

export N_PREFIX=/opt/homebrew
export PATH="$N_PREFIX/bin:$PATH"

source ~/.zshrc

n install 16.15.0
node -v
n install v21.6.2
n # select version of node
node -v # 21.6.2
```


## Install npm
As we know earlier, npm is the default package manager for Node.js. It is used to install, publish, and manage node programs. 
```bash
npm install # but failed
```
npm is just like pip in python. It is a package manager for JavaScript.

Then I encounter with several problems. Firstly, I cannot download from github. I need to use ssh to download the package. 
The detailed solution is here <a href="[https://jiangxunyi.github.io/post/command-lines/" title="mypost">My note for ssh</a>
I cannot install gyp because of my python version, here is the explanation <a href="https://stackoverflow.com/questions/33896511/npm-install-fails-with-node-gyp" title ="StackOverFlow Solution">StackOverFlow Solution</a>
My python version is 3.12.0, too high!

So the solution is to find the suitable python version.

I also found that I cannot use conda in zsh, so I set
```bash
export PATH="opt/miniconda3/bin:$PATH"
```
Then I can use conda in zsh.
Recall how to create environment in conda
```bash
conda create -n node python=3.10
conda activate node
```
Then I can use this python version to install gyp
```bash
npm install
```
Then I can install the package successfully.
```bash
npm run dev
```
Then I can run the project successfully.

# JavaScript Grammar
## Grammar and types
- comment: // /* */
### Declarations
- var: function-scoped, declares a variable, optionally initializing it to a value.
- let: block-scoped, declares a block-scoped, local variable, optionally initializing it to a value.
- const: block-scoped, declares a block-scoped, <span style="color:pink">read-only</span> named constant.

identifier: A name that identifies a variable, function, or property. Starts with a letter, underscore, or dollar sign. Subsequent characters can also be digits (0-9). Case sensitive.

declare variables to unpack values:
You can use destructuring assignment syntax to declare variables and unpack values from an object. Specifically, the code `const { bar } = foo`; extracts the value of the bar property from the object foo and assigns this value to a variable named bar.

Here is a detailed explanation:

Suppose there is an object foo, whose structure might look like this: const foo = { bar: 42, baz: 'hello' };.
When you write const { bar } = foo;, JavaScript will find the property named bar in the object foo and assign its value (42 in this example) to a new variable bar.
The result is that you now have a variable bar with a value of 42, which is the same as the value of the bar property in the foo object.

### Data types are similar to Python
With all other operators, JavaScript does not convert numeric values to strings. For example:

JS
Copy to Clipboard
"37" - 7; // 30
"37" * 7; // 259

# Development
If I want to check the sessionStorage, I can use `option + cmd + i` to open the console at Google Chrome. Then `Application > Storage > sessionStorage > key`
I found the data is like: 
```jsonr
{
  "project-set-dashboard-project-new": "Y",
  "project-set-create": "Y",
  "project-set-edit": "Y",
  "project-set-launch": "Y",
  "role-dashboard-details": "Y",
  "role-dashboard-delete": "Y",
  "payment-entry-and-summary-return": "Y",
  "payment-and-invoice-department-data": "Y",
  "homepage-project-manager-homepage": "Y",
  "homepage-office-homepage": "Y"
}
```
Then I use `shift + cmd + F` to search globally to find out where this item is set. I use `sessionStorage.setItem(` to search.
Then I found the code:
```JavaScript
routeData = Object.assign({}, obj)
      if (routeData !== null) {
        Vue.set(asyncRoutes[0], 'hidden', routeData['budget-preparation-menu'] !== 'Y')
        Vue.set(asyncRoutes[1], 'hidden', routeData['project-library-menu'] !== 'Y')
      }
```
I can use `Vue.set` to set the value of the object.