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
  - 开源

categories:
  - Study Notes

enable_math: True
---
# Node.js Basic Knowledge
## Node.js
Node.js is a free, open-source, cross-platform JavaScrip runtime evnvironment that lets developers to create servers, web apps, command line tools and scrips.
I ananogy this with python interpreter, or Java interpreter.

## npm: node package management
本篇note主要从 <a href="[超链接地址](https://www.freecodecamp.org/chinese/news/what-is-npm-a-node-package-manager-tutorial-for-beginners/)" title="这篇博客：什么事npm-写给初学者">这篇博客：什么事npm-写给初学者</a>
npm 是JavaScript运行时Node.js 的默认程序包管理器，主要有两个部分组成：
- 用于发布和下载程序包的CLI（命令行界面）工具
- 托管JavaScript程序包的在线储存库
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
my python version is 3.12.0, too high!

So the solution is to find the suitable python version.

I also find that I cannot use conda in zsh, so I set
```bash
export PATH="opt/miniconda3/bin:$PATH"
```
Then I can use conda in zsh.
Recall how to create env in the conda
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

identifier: A name that identifies a variable, function, or property. Starts with a letter, underscore, or dollar sign. Subsequent characters can also be digits (0-9). Case sentitive.

declare variables to unpack values:
你可以使用解构赋值语法来声明变量，并从一个对象中解包值。具体来说，`const { bar } = foo`; 这段代码会从对象 foo 中取出 bar 这个属性的值，并将这个值赋给一个名为 bar 的变量。

以下是详细解释：

假设有一个对象 foo，它的结构可能是这样的：const foo = { bar: 42, baz: 'hello' };。
当你写 const { bar } = foo; 时，JavaScript 会找到对象 foo 中名为 bar 的属性，并将它的值（在这个例子中是 42）赋给一个新的变量 bar。
结果是，你现在有了一个变量 bar，它的值是 42，与 foo 对象中的 bar 属性的值相同。

### Data types 就跟python类似
With all other operators, JavaScript does not convert numeric values to strings. For example:

JS
Copy to Clipboard
"37" - 7; // 30
"37" * 7; // 259

# Development
If I want to check the sessionStorage, I can use `option + cmd + i` to open the console at Google Chrome. Then `Application > Storage > sessionStorage > key`
I find the data is like: 
```jsonr
{
  "项目集看板-项目新增": "Y",
  "项目集-创建": "Y",
  "项目集-编辑": "Y",
  "项目集-启动": "Y",
  "角色看板-详情": "Y",
  "角色看板-删除": "Y",
  "付款录入及汇总-退回": "Y",
  "付款与发票-部门数据": "Y",
  "首页-项目经理首页": "Y",
  "首页-办公室首页": "Y"
}
```
then I use `shift + cmd + F` to search globally to find out where set this item. I use `sessionStorage.setItem(` to search.
Then I found the code:
```JavaScript
routeData = Object.assign({}, obj)
      if (routeData !== null) {
        Vue.set(asyncRoutes[0], 'hidden', routeData['预算编制-菜单'] !== 'Y')
        Vue.set(asyncRoutes[1], 'hidden', routeData['项目库-菜单'] !== 'Y')
      }
```
I can use `Vue.set` to set the value of the object.