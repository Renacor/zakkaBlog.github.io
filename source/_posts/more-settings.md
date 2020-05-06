---
title: HEXO更多配置
tags: 配置
categories: HEXO
---
实际使用一个主题时，有很多常用的细节上的配置在主题初始时并不会设置好，需要手动找到配置文件中相对应的项进行设置，以目前我正在使用的NextT主题为例,记录下如何进行细节配置。
<!-- more -->
#### 显示语言设置
#### 首页不显示全文
在文章内需要截断的地方添加上标记
```html
首页会显示的text1111
<!-- more -->
在首页会隐藏的text22222
```
#### 首页出现菜单内容以及菜单内容对应路径文件

#### 文章添加分类和tag
在文章的开头指定配置tag和分类即可，如
```yml
---
tags: 配置 // tag
categories: HEXO // 分类
---
```
#### 文章插入图片
把主页配置文件 *_config.yml* 里的 *post_asset_folder*这个选项设置为true
在hexo的目录下执行<code>npm install https://github.com/CodeFalling/hexo-asset-image --save</code>（需要等待一段时间）。
完成安装后用<code>hexo n "nnn"</code>新建文章的时候会发现 *_posts* 目录下面会多出一个和文章名字一样的文件夹。图片就可以放在文件夹下面
#### 修改样式和添加自定义样式
打开文件： *根目录\themes\[themeName]\source\css\_custom\custom.styl*,在该文件中自定义样式
#### 文章字数统计和预计阅读时长
字数统计和预计阅读市场需要在两处进行配置
nextT自带的字数统计工具是*hexo-symbols-count-time*，首先需要确认已安装
```
npm install hexo-symbols-count-time --save // 安装hexo-symbols-count-time
```
**配置项修改**
首先在博客的根目录下的配置文件 *_config.yml* 里配置以下内容
```yml
symbols_count_time:
 #文章内是否显示
  symbols: true
  time: true
 # 网页底部是否显示
  total_symbols: true
  total_time: true
```
然后在主题的配置文件中配置以下内容,具体参数意义详见[hexo-symbols-count-time](https://github.com/theme-next/hexo-symbols-count-time)
```yml
symbols_count_time:
  separated_meta: true
  #文章中的显示是否显示文字（本文字数|阅读时长） 
  item_text_post: true
  #网页底部的显示是否显示文字（站点总字数|站点阅读时长） 
  item_text_total: false
  # Average Word Length (chars count in word)
  awl: 4
  # Words Per Minute
  wpm: 275
```
#### 评论，打赏，RSS功能
#### 广告位(X
#### 配置live2d宠物
#### 文章首页完美隐藏
下载hexo-generator-index2插件后卸载官方的插件hexo-generator-index
```
$ npm install hexo-generator-index2 --save
$ npm uninstall hexo-generator-index --save
```

打开根目录的`_config.yml`，在末尾添加一下内容，注意空格和缩进
```yml
# index2 generator是否包含官方的hexo-generator-index，默认true（包含）
index2_include_index: true
index2_generator:
	per_page: 8
	order_by: -date
	exclude:
		- tag hide
		- category hide
```
`exclude`:表示隐藏哪些内容，以上代码表示隐藏tag为hide和category(分类)为hide的文章

[hexo-helper-live2d](https://github.com/EYHN/hexo-helper-live2d/blob/master/README.zh-CN.md)