---
title: hexo、GitHub搭建个人博客网站
date: 2024-01-25 13:29:20
tags:
cover: ./pics/blogPics/tree.jpg
top_img: #3DA0F2
description: 如何使用hexo搭建个人博客
---

# hexo、GitHub搭建个人博客网站

<p>操作系统：macOS Ventura 13.1</p>

> 可谓是，克服了万难啊！

---

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

  - ```
    // 安装hexo
    npm install hexo -g
    
    // 建立目标文件夹
    hexo init blog
    
    // 进入目标文件夹
    cd blog
    
    // 安装依赖
    npm install
    
    // 打开博客
    hexo serve
    ```

  - 这里就可以得到本地的网站地址了。
    - ``Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.``

---

## 第二部分：hexo配置到github

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
  >
  > repo为``https://github.com/GITHUBID/GITHUB.github.io.git``,
  >
  > branch为``main``
  >
  > 但我没能成功

### 4. hexo部分

- ```
  // 安装插件
  npm install --save hexo-deployer-git
  
  // 构建hexo框架
  hexo clean
  hexo g 
  hexo d
  ```

- Hero g是hexo generate

- hexo d是hexo deploy

### 5. 问题排查

> 如果按照以上的操作没有报错的话，恭喜你是一个幸运儿，而我在将hexo部署到github上时遇到了很多的问题

#### hexo d报错：

1. 超时
   1. fatal: unable to access ``https://github.com/xxx/xxx.github.io``
2. 要求输入username和password
   1. 压根不知道要输入什么username和password
3. 端口关闭
   1. kex_exchange_identification: Connection closed by remote host Connection close
4. fatal: unable to connect to github.com:github.com[0: 20.205.243.166]: errno=Operation timed out

#### 解决方案：

**配置了repositoty的SSH密钥**

```
// 1.输入邮箱，生成密钥，命令的目的是为了让本地机器ssh登录远程机器上的GitHub账户无需输入密码
ssh-keygen -t rsa -C "youremail@example.com"

// 2. 将SSH key 添加到 ssh-agent
ssh-add ~/.ssh/id_rsa

// 3. 将SSH key 添加到你的GitHub账户
// 这一步回到github，在repo中新建一个ssh密钥，粘贴d_rsa.pub文件中的内容生成

// 4. 验证key
ssh -T git@github.com
```

若出现：``You've successfully authenticated, but GitHub does not provide shell access.``则是验证成功了，至此，直接解决了以上问题。

### 6. github查看

- 一看code界面是否展示了上传上去的文件夹
- 二就可以打开``xxxx.github.io``查看自己博客的最初样子了

---

