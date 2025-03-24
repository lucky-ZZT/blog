---
title: 博客搭建流程（hexo-netlify-github）
abbrlink: 359ff663
date: 2023-04-09 23:21:49
tags: hexo博客搭建
cover:
swiper_index: 1
category: 博客搭建
---

# 搭建个人博客过程(hexo博客框架)

>参考自：[爱扑bug的熊](https://blog.cuijiacai.com/blog-building/)
>
>https://blog.cuijiacai.com/blog-building/

## 1.配置环境

>安装nodejs
>
>- windows直接在官网安装
>- OS或者liux使用相应命令进行安装



>安装完成后查看版本信息：
>
>```
>node -v # 查看node版本信息
>npm -v # 查看npm版本信息（npm是nodejs的包管理器）
>```



>换源（默认源速度较慢）：
>
>```
>
>npm config get registry # 查看原来的源
>npm config set registry https://registry.npmmirror.com # 修改为淘宝源，可能失效
>npm config get registry # 查看现在的源
>```

## 2.生成博客

>安装HEXO
>
>```
>npm install hexo-cli -g # 全局安装hexo命令行工具
>```

>初始化博客
>
>```
>hexo init "你的博客目录名称" # 目录名称不含空格的时候双引号可以省略
>cd "博客目录"  # 进入博客目录
>npm install # 安装需要的其他支持，安装的依赖项在package.json文件的dependencies字段中可以看到
>```

>博客项目目录简介：
>
>windows可使用dir命令查看
>
>```
>.
>├── _config.landscape.yml
>├── _config.yml
>├── node_modules
>├── package-lock.json
>├── package.json
>├── scaffolds
>├── source
>└── themes
>```
>
>- ```
>  _config.yml
>  ```
>
>  - 为全局配置文件，网站的很多信息都在这里配置，比如说网站名称，副标题，描述，作者，语言，主题等等。具体可以参考官方文档：https://hexo.io/zh-cn/docs/configuration.html。
>
>- ```
>  scaffolds
>  ```
>
>  - 骨架文件，是生成新页面或者新博客的模版。可以根据需求编辑，当`hexo`生成新博客的时候，会用这里面的模版进行初始化。
>
>- ```
>  source
>  ```
>
>  - 这个文件夹下面存放的是网站的`markdown`源文件，里面有一个`_post`文件夹，所有的`.md`博客文件都会存放在这个文件夹下。现在，你应该能看到里面有一个`hello-world.md`文件。
>
>- ```
>  themes
>  ```
>
>  - 网站主题目录，`hexo`有非常丰富的主题支持，主题目录会存放在这个目录下面。
>  - 我们后续会以默认主题来演示，更多的主题参见：https://hexo.io/themes/

>测试：
>
>```
>hexo new post "test" # 会在 source/_posts/ 目录下生成文件 ‘test.md’，打开编辑
>hexo generate        # 生成静态HTML文件到 /public 文件夹中
>hexo server          # 本地运行server服务预览，打开 http://localhost:4000 即可预览你的博客
>```
>
>出现问题：command not found
>```
>npx hexo +命令
>```

>更详细的`hexo`命令可以查看文档：https://hexo.io/zh-cn/docs/commands

>完善建站脚本：
>
>```
>{
>    // ......
>    "scripts": {
>        "build": "hexo generate",
>        "clean": "hexo clean",
>        "deploy": "hexo deploy",
>        "server": "hexo server",
>        "netlify": "npm run clean && npm run build" // 这一行为新加，作用是清理旧的网站文件，再生成新的网站文件
>    },
>    // ......
>}
>```

>配置信息（_config.yml）：
>
>```
># Site
>title: Hexo  # 网站标题
>subtitle:    # 网站副标题
>description: # 网站描述
>author: John Doe  # 作者
>language:    # 语言
>timezone:    # 网站时区, Hexo默认使用您电脑的时区
>
># URL
>## If your site is put in a subdirectory, set url as 'http://yoursite.com/child'
>## and root as '/child/'
>url: http://yoursite.com   # 你的站点Url
>root: /                    # 站点的根目录
>permalink: :year/:month/:day/:title/   # 文章的 永久链接 格式   
>permalink_defaults:        # 永久链接中各部分的默认值
>
># Directory   
>source_dir: source     # 资源文件夹，这个文件夹用来存放内容
>public_dir: public     # 公共文件夹，这个文件夹用于存放生成的站点文件。
>tag_dir: tags          # 标签文件夹     
>archive_dir: archives  # 归档文件夹
>category_dir: categories     # 分类文件夹
>code_dir: downloads/code     # Include code 文件夹
>i18n_dir: :lang              # 国际化（i18n）文件夹
>skip_render:                 # 跳过指定文件的渲染，您可使用 glob 表达式来匹配路径。    
>
># Writing
>new_post_name: :title.md  # 新文章的文件名称
>default_layout: post      # 预设布局
>titlecase: false          # 把标题转换为 title case
>external_link: true       # 在新标签中打开链接
>filename_case: 0          # 把文件名称转换为 (1) 小写或 (2) 大写
>render_drafts: false      # 是否显示草稿
>post_asset_folder: false  # 是否启动 Asset 文件夹
>relative_link: false      # 把链接改为与根目录的相对位址    
>future: true              # 显示未来的文章
>highlight:                # 内容中代码块的设置    
>  enable: true            # 开启代码块高亮
>  line_number: true       # 显示行数
>  auto_detect: false      # 如果未指定语言，则启用自动检测
>  tab_replace:            # 用 n 个空格替换 tabs；如果值为空，则不会替换 tabs
>
># Category & Tag
>default_category: uncategorized
>category_map:       # 分类别名
>tag_map:            # 标签别名
>
># Date / Time format
>## Hexo uses Moment.js to parse and display date
>## You can customize the date format as defined in
>## http://momentjs.com/docs/#/displaying/format/
>date_format: YYYY-MM-DD     # 日期格式
>time_format: HH:mm:ss       # 时间格式    
>
># Pagination
>## Set per_page to 0 to disable pagination
>per_page: 10           # 分页数量
>pagination_dir: page   # 分页目录
>
># Extensions
>## Plugins: https://hexo.io/plugins/
>## Themes: https://hexo.io/themes/
>theme: landscape   # 主题名称
>
># Deployment
>## Docs: https://hexo.io/docs/deployment.html
>#  部署部分的设置
>deploy:     
>  type: '' # 类型，常用的git 
>```

## 3.github项目文件托管

>git使用：
>
>![git流程](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/git%E6%B5%81%E7%A8%8B.png)
>
>```
>git init  # 创建本地仓库
>git add .  # 工作区提交至暂存区
>git commit -m "my blog first commit"  # 暂存区提交至仓库区
>git remote add origin "远端github仓库地址"
>git branch -M main
>git push -u origin main
>```
>
>git log 查看日志
>
>git reset 回退版本
>
>git config 配置个人信息

>github使用:
>
>上传权限问题：生成ssh秘钥，并放入github中
>
>![image-20230407171835074](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/github%E6%B5%81%E7%A8%8B.png)

>**注意事项：**
>
>更改主题时，必须删除上传到GitHub里的主题文件的**.git**文件

## 4.netlify建站

>1. 首先注册并登陆
>
>  [Netlify](https://app.netlify.com/)官网
>
>  - 这一步需要能够科学上网，因为这是一个国外的网站
>  - 我们的博客在开启cloundflare的CDN加速之前，也只能通过科学上网的方式访问
>
>2. 新建站点：
>
>   ![create-site](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/SJvGYlIzZVm7iP5.png)
>
>3. 连接
>
>  ```
>  github
>  ```
>
>- ![connect-github](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/oSa6BOtIQ8WkZX1.png)
>
>4. 选择刚刚上传的博客项目：
>
>  - ![select-project](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/e2sGfOYSAFPylVB.png)
>
>5. 一切默认，除了构建命令改成我们之前设置的
>
>  ```
>  npm run netlify
>  ```
>
>  - ![site-config](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/p3P2NJaQzuIZnYs.png)
>
>    > 这里BaseDirectory为空表示项目目录是仓库目录的根目录。
>
>6. 构建完成后我们就能够看到一个URL，打开网址就是我们的个人博客了
>
>  - ![url-generate](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/B2qmolnIgDH5uNt.png)
>
>可以根据提示进行进一步的设置，比如说设置一下二级域名（即`netlify.app`之前的域名）。
>
>在下面的演示中，我设置的`netlify`二级域名为`blogbearsir`，也就是说，我的个人博客站点的域名为`blogbearsir.netlify.app`。
>
>不过现在，我们的个人博客已经算是搭建完成了。下面需要解决的就是配置域名和访问慢的问题了。

>**中间出现问题**：解决办法，==pakeage.json==格式问题。以及未按要求修改设置

### 配置域名：

>1. 在netlify设置用户域名。
>   - ![set-custom-domain](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/MDjxbIcWBEoLURA.png)
>2. 进行相关的配置，由于我们的域名本身已经配置了解析，这里会显示出来，不用再额外添加记录，只需要一路默认即可。
>   - ![add-record](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/cqwL9xF8Eov6yVa.png)
>   - ![activate-dns](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/RTLcjynQYXbW9vI.png)
>3. 设置一下netlify本身的对于国外CDN的支持。
>   - ![netlify-cdn](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/8v3ROjQc2WY9q7T.png)
>
>之后，我们就可以通过自己配置的域名访问自己的个人博客，比如说我的博客地址是 [https://blog.cuijiacai.com](https://blog.cuijiacai.com/) 。
>
>> 这里`https`访问需要在`netlify`中配置，否则应该只能`http`访问。
>> ![https-config](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/f3q8hPbG5vsImeY.png)
>> 需要注意一下的是，此刻的https配置过程中的dns验证已经可以通过，但是证书检查会失败，等到后面clouldflare加速配置完成之后，这个问题 就可以解决了。所以暂时应该只能http访问。
>
>但是，此刻我们的博客访问依然需要科学上网，因为我们还没有国内的CDN的支持，下面，我们来解决这个问题。

## ClouldFlare加速

>## 介绍
>
>Netlify 虽然已经提供了 CDN 加速，但在使用过程中发现国内访问还是比较慢，Cloudflare 相对于国内的七牛云、阿里云等云服务商的 CDN 速度会慢一些，但是它有免费版本，而且最重要的是域名不用备案。
>
>## 加速步骤
>
>1. 注册[Clouldflare](https://www.cloudflare.com/zh-cn/)并登陆
>2. 添加站点
>   - ![add-site](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/rqNObP5dzE6GY83.png)
>   - ![config-site](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/Dk3Y4BrltQeCOHI.png)
>3. 选择免费套餐
>   - ![choose-project](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/SrhEAvmGZeqn8Co.png)
>4. 添加 DNS 记录
>   - 一般情况下 Cloudflare 会检测出来几条 DNS 记录，类型大多数是A，或者AAAA，由于我们是转发，所以应该是 CNAME 类型才对。有必要的话可能得手动配置一下。
>   - ![update-record](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/fSsAGV5JCeZuF1w.png)
>5. 更改名称服务器
>   - 这个步骤Cloudflare会提供一个在线的教程，主要步骤是在你的域名服务商那里修改 dns 解析服务器为 cloudflare 提供的地址，修改完成后点击完成。
>   - ![modify-server](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/vd2WxXGbJHmgAey.png)
>   - 以阿里云为例，设置的步骤如下:
>     1. 进入域名的配置界面
>        - ![dns-manage](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/ZfLiNUejRsCyhG3.png)
>     2. 将域名服务器从阿里云的默认服务器改成clouldflare的服务器
>        - ![change-server](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/juxWl7i9QaeLTGK.png)
>   - 配置完成后，clouldflare会有邮件通知(一般不会等太久)
>     ![mail-notice](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/JbBvp18Trne37kC.png)

## 配置https

>在clouldflare配置完成之后，我们可以回到netlify去配置一下https访问。
>
>1. 先确认一下dns解析:
>   - ![verify-dns](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/r6iHKWLktnRap1j.png)
>2. 然后自动安装证书:
>   - ![certify](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/KvDupBFh8b9CScN.png)
>3. 最后看到如下的界面，就说明https配置完成了:
>   - ![https-config](https://ztblog-image.oss-cn-chengdu.aliyuncs.com/f3q8hPbG5vsImeY.png)
