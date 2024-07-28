---
title: hexo搭建个人博客网站
date: 2024-01-30 18:59:14
categories: Computer
tags: Web
keywords: 'web, hexo'
description: 使用hexo框架在github上搭建个人博客网站。
cover: shore.jpg
# top_img : 'linear-gradient(20deg, #0062be, #925696, #cc426e, #fb0347)'
---

# hexo、GitHub搭建个人博客网站

<p>操作系统：macOS Ventura 13.1</p>

> 前言：可谓是，克服了万难啊!

![封面](1.png)

## 第一步：环境配置
- Node.js

  - 官网下载pkg文件，安装包安装
  - 安装验证：``node -v``

- npm

  - 安装Node的时候同时就安装好了
  - 安装验证：``npm -v``

- git

  - 官网下载pkg文件，安装包安装
  - 安装验证：``git version``

- hexo

    - 安装hexo
    npm install hexo -g
    hexo init blog
    
    - 进入目标文件夹
    cd blog
    
    - 安装依赖
    npm install
    
    - 打开博客
    hexo serve

    - 这里就可以得到本地的网站地址了。
    ``Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.``


## 第二步：hexo部署到github

### 1. github准备

- 注册github账号
- 创建新的的库(repository)
  - 库的名称一定是``ID``.github.io
  - 可见性是public

### 2. git设置

- 设置用户名和邮箱

  - ```
    git config --global user.name "YOURNAME"
    git config --global user.email "YOUREMAIL"
    ```

### 3. _config.yml文件的配置

- 在最底部的deploy部分添加：

  - ```
    deploy:
    	type: 'git'
    	repo: 'git@github.com:GITHUBID/GITHUBID.github.io.git'
    	branch: 'master'
    ```

  > 有的教程
  > repo为``https://github.com/GITHUBID/GITHUB.github.io.git``,
  > branch为``main``
  > 但我没能成功

### 4. 代码备份

### 5. hexo部分

- 安装插件
    ``npm install --save hexo-deployer-git``
  
- 构建hexo框架
```  
  hexo clean
  hexo g 
  hexo d
  ```
  
### 6.（如果遇到报错）hexo d报错：

1. 超时
   1. fatal: unable to access ``https://github.com/xxx/xxx.github.io``
2. 要求输入username和password
   1. 压根不知道要输入什么username和password
3. 端口关闭
   1. kex_exchange_identification: Connection closed by remote host Connection close
4. fatal: unable to connect to github.com:github.com[0: 20.205.243.166]: errno=Operation timed out

#### 解决方案：

**配置了repositoty的SSH密钥**

```shell
# 1.输入邮箱，生成密钥，命令的目的是为了让本地机器ssh登录远程机器上的GitHub账户无需输入密码
ssh-keygen -t rsa -C "youremail@example.com"

# 2. 将SSH key 添加到 ssh-agent
ssh-add ~/.ssh/id_rsa

# 3. 将SSH key 添加到你的GitHub账户
// 这一步回到github，在repo中新建一个ssh密钥，粘贴d_rsa.pub文件中的内容生成

# 4. 验证key
ssh -T git@github.com
```

- 若出现：``You've successfully authenticated, but GitHub does not provide shell access.``则是验证成功了，至此，直接解决了以上问题。


### 7. github查看

- 一看code界面是否展示了上传上去的文件夹
- 二就可以打开``xxxx.github.io``查看自己博客的最初样子了

---
## 使用中学习
### 1. hexo框架结构
![hexo框架结构](2.png)
- ``scaffolds``：文件上传的默认模版
- ``source``：包括博客、图片等等

## 后续填坑：

时隔三个月重新在新电脑上配置hexo环境，步骤如下：
- 安装vscode
- 安装python
  - 现在这俩东西都可以在安装的时候选择添加到path，省去了很多功夫
  - 关于安装路径：在安装这一类程序的时候，可以将盘符直接改为D盘即可，将其规范地放到非系统盘里
- 安装git
- 将vscode直接与github相连，就可以很快地clone某一个库
- 安装nodejs、npm、hexo
  - 在使用hexo的时候遇到了一个问题：`hexo : 无法加载文件 C:hexo.ps1，因为在此系统上禁止运行脚本`
  - [解决方案](https://www.cnblogs.com/hdlan/p/14452703.html)
- 加入了一些新的内容，但无法上传（`hexo d`）
  - 问题原因：`git@github.com: Permission denied (publickey)`
  - [解决方案](https://blog.csdn.net/qq_40047019/article/details/122898308)
    - 方案解读：
      - 确定路径：打开文件夹C:\Users\Administrator\.ssh（Administrator是当前用户名），在空白处点鼠标右键选择“Git Bush Here” ，打开gitbush。
      1. 生成密钥：`ssh-keygen -t rsa -C "xx@example.com"`， youremail@example.com改为自己的邮箱
      2. 添加密钥：`ssh-add ~/.ssh/id_rsa`
        - 如果不行尝试eval `ssh-agent -s`后使用`ssh-add ~/.ssh/id_rsa`
      3. 在github添加新的SSH密钥：将id_rsa.pub里的内容添加到github的设置中
      4. 验证：`ssh -T git@github.com`

## 参考链接
[1. markdown中图片的处理](https://blog.csdn.net/2301_77285173/article/details/130189857)
[2. butterfly配置文档](https://butterfly.js.org/posts/21cfbf15/)


