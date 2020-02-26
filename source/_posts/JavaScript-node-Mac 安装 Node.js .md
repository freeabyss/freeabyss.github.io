---
title: Mac 下安装 Node.js
date: 2017-03-25 19:47:43
tags: [JavaScript,  Node]
categories: [Node]
---

## 前言

安装 Node.js （以下简称node）有很多种方式。在 Mac 下常用的方式是使用 Homebrew 进行安装。不过由于 node 更新频繁，在开发过程中很有可能会有切换 node 版本的需求，因此建议使用 nvm 安装管理 node。Homebrew 上面虽然有 nvm 但是官方不建议使用 Homebrew 进行安装。我也用过 Homebrew 安装过，不过容易出问题，最终又卸载了。 

本文包括两方面内容： 

*  安装 nvm
* 使用 nvm 管理 node 版本

## 安装 nvm

如果用过 Homebrew 安装过 nvm 建议您卸载了，`brew uninstall nvm`

详细的安装流程可以参阅官方文档 [nvm](https://github.com/creationix/nvm)

安装命令如下： 

```shel
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash
```

安装完毕后，不需要额外的配置即可使用 ，以下内容会被自动的添加到 profile 文件中

```shell
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
```

## 使用 nvm 管理 Node.js

nvm 切换 node 版本的原理无非通过是修改环境变量，指向不同版本的 node 所在的路径。

以下是常有的 nvm 命令，更多命令参考 [nvm github 地址](https://github.com/creationix/nvm/blob/master/README.markdown)

`nvm ls-remote` 查看可安装的版本

`nvm install <version>` 安装指定版本的 node

` nvm ls`  列出目前安装的版本

`nvm use <version>` 切换版本，`use`  命令只对当前 shell 窗口有效

`nvm alias default <version>` 设置默认的 node 版本，对所有 shell 窗口有效

`nvm install node`  安装最新的node

`nvm use node`  使用最新的node

