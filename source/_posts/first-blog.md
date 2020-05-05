---
title: First Blog
tags: 配置
categories: HEXO
---
记录博客配置的全过程。
 <!-- more -->
#### 前置准备
1. node.js和npm
2. git

#### 安装HEXO
```
$ npm install -g hexo-cli  
$ npm install hexo-server --save
```
#### 新建项目并运行

```
$ hexo init blog
$ cd blog
$ npm install
$ hexo server
```
至此博客项目新建完成

#### 更换主题
1. 找到喜欢的主题的github地址
```
	cd blog
	git clone https://github.com/theme-next/hexo-theme-next themes/NewThemeName
	cd themes/NewThemeName
	git pull 
```
	
2. 主题修改配置
修改blog目录下的 _config.yml ： theme: NewThemeName


#### 配置GitHub
1. 申请一个github账号且完成邮箱验证
2. 新建Repository(仓库)
3. 新仓库的名称命名格式[^1]：
```
用户名.github.io
```
[^1]: 名称后缀是固定的，不可更改。当配置完成后在github访问域名时，如进去的页面显示404，解决的方法为：①配置个人域名②仓库的名称改为github的用户名
4. 配置git信息
```
git config --global user.name"这里是你申请Github账号时的name"
git config --global user.email"这里是你申请Github账号时的邮箱"
```
5. 部署。进入blog目录下,编辑 _config.yml，把下面的your_username换成你的github用户名，注意冒号后面有一空格。
```
deploy:
    type: git
    repo: https://github.com/your_username/your_username.github.io.git
    branch: master
```
#### 部署代码到Github
```
$ hexo clean // 清除缓存文件 (db.json) 和已生成的静态文件 (public)。
$ hexo d -g // 生成静态文件并部署
```
#### 发布新文章
新建文章推荐使用命令行执行<code>hexo n "newFileName"</code>，也可直接编辑器打开项目，在*source/_posts*目录下新建.md文章

生成静态文件: <code>hexo g</code>
提交到github: <code>hexo d</code>

####  添加版权说明
在*themes\hiker\layout\_partial新建文件copyright.ejs*
打开*copyright.ejs*,添加一下内容。
```html
<div>
        <ul class="post-copyright">
          <li class="post-copyright-author">
          <strong><%= __('copyright.author') %> </strong><%= config.author%></a>
          </li>
          <li class="post-copyright-link">
          <strong><%= __('copyright.link') %> </strong>
          <a href="<%- config.root %><%- post.path %>" target="_blank" title="<%= post.title %>"><%- config.url %>/<%- post.path %></a>
          </li>
          <li class="post-copyright-license">
            <strong><%= __('copyright.license_title') %>  </strong>
            <%= __('copyright.left_license_content') %><a rel="license" href="https://creativecommons.org/licenses/by-nc-nd/4.0/" target="_blank" title="Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)">CC BY-NC-ND 4.0</a>
            <%= __('copyright.right_license_content') %>
          </li>
        </ul>
      <div>
```
	
打开*themes\hiker\layout\_partial\article.ejs*添加一下内容,位置介于*donate*和c*omment*之间
	
```html
	<% if (!index && theme.donate.enable){ %>
	        <%- partial('donate') %>
	      <% } %>
	       <!-- 要添加的内容 -->
	      <% if (!index && theme.copyright.enable){ %>
	      <%- partial('copyright') %>
	      <% } %>
	      <!---->
	      <% if (!index && post.comments && (theme.gentie_productKey || theme.duoshuo_shortname || theme.disqus_shortname || theme.uyan_uid || theme.wumii || theme.livere_shortname)){ %>
	        <%- partial('comment') %>
	      <% } %>
```
	
修改*themes\hiker\source\css\_partial\article.styl*,在末端添加以下内容。
	
```css
	.post-copyright {
	    margin: 2em 0 0;
	    padding: 0.5em 1em;
	    border-left: 3px solid #FF1700;
	    background-color: #F9F9F9;
	    list-style: none;
	}
	
	.post-copyright li {
	    line-height: 30px;
	}
```
在*themes\hiker\languages*中,找到你应用的语言文件,例如zh-TW,打开并添加以下内容。
```yml
copyright:
    author: "作者: "
    link: "文章连结: "
    license_title: "版权声明: "
    left_license_content: "本网志所有文章除特别声明外,均采用 "
    right_license_content: "许可协议。转载请注明出处!"
```
打开*themes\hiker\_config.yml*,添加以下内容。
```yml
#版权信息
copyright:
    enable: true
```


#### markdown解析器替换
hexo自带的markdown解析器为GFM风格，与标准的markdown语法有些许不同且支持的语法较少，往往无法满足更专业的需求。
hexo-renderer-markdown-it 是一款用于 Markdown 解析和渲染的插件。
- 用于替换 Hexo 默认自带的 Markdown 渲染器。
- 提供了更丰富的 Markdown 解析和渲染。

**首先请确保以下操作是在博客项目的根目录进行**
```
npm un hexo-renderer-marked --save // 卸载 Hexo 默认自带的 Markdown 渲染器
npm i hexo-renderer-markdown-it --save // 安装 hexo-renderer-markdown-it 插件
```
打开根目录下的_config.yml
```yml
# Markdown-it config
markdown:
  render:
    html: true
    xhtmlOut: false
    breaks: true
    linkify: true
    typographer: true
    quotes: '“”‘’'
  plugins:
    - markdown-it-abbr
    - markdown-it-footnote
    - markdown-it-ins
    - markdown-it-sub
    - markdown-it-sup
  anchors:
    level: 2
    collisionSuffix: 'v'
    permalink: true
    permalinkClass: header-anchor
    permalinkSymbol: ¶
```