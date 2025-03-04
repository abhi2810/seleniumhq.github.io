---
title: 为 Selenium 文档做贡献
linkTitle: 为 Selenium 文档做贡献
weight: 2
aliases: 
        [
          "/documentation/zh-cn/contributing/",
          "/documentation/zh-cn/front_matter/typographical_conventions/"
        ]
---


{{% pageinfo color="warning" %}}
<p class="lead">
   <i class="fas fa-language display-4"></i> 
   Page being translated from 
   English to Chinese. Do you speak Chinese? Help us to translate
   it by sending us pull requests!
</p>
{{% /pageinfo %}}

Selenium是一个大型软件项目, 
其网站和文档是了解事情如何工作以及学习有效利用其潜力的关键.

该项目包含Selenium的网站和文档. 
这是一项持续的工作(不针对任何特定版本), 
用于提供有效使用Selenium、
如何参与以及如何为Selenium做出贡献的更新信息.

对网站和文档的贡献遵循以下部分中有关贡献的描述. 

---

Selenium项目欢迎每一个人的贡献. 
您可以通过多种方式提供帮助:

## 上报问题

在报告新问题或评论现有问题时, 
请确保讨论与Selenium的软件、
其站点与文档的具体技术问题相关.

随着时间的推移, 所有Selenium组件的变化都非常快, 
因此这可能会导致文档过时. 
如前所述, 如果您确实遇到这种情况, 请不要为此担心. 
您也可能知道如何更新文档, 因此请向我们发送包含相关更改的Pull Request.

如果不确定所发现的问题是否存在, 请通过以下沟通渠道进行描述 
https://selenium.dev/support.

## 贡献

Selenium项目欢迎新的贡献者. 
随时间做出重大贡献的个人将成为 _提交者_ , 并获得对该项目的提交权限.

本指南将指导您完成贡献的过程.

### 步骤 1: Fork

在 [Github](https://github.com/seleniumhq/seleniumhq.github.io)上Fork本项目, 
并check out到您的本地


```shell
% git clone git@github.com:seleniumhq/seleniumhq.github.io.git
% cd seleniumhq.github.io
```

#### 依赖: Hugo

We use [Hugo](https://gohugo.io/) and the [Docsy theme](https://www.docsy.dev/)
to build and render the site. You will need the “extended” 
Sass/SCSS version of the Hugo binary to work on this site. We recommend
to use Hugo 0.83.1 or higher.

Please follow the [Install Hugo](https://www.docsy.dev/docs/getting-started/#install-hugo) 
instructions from Docsy.

### 步骤 2: 分支

创建一个功能分支并开始工作:

```shell
% git checkout -b my-feature-branch
```

我们实践基于HEAD的开发模式, 这意味着所有更改都直接应用在trunk之上.

### 步骤 3: 做出改变

The repository contains the site and docs. Before jumping into
making changes, please initialize the submodules and install the
needed dependecies (see commands below). To make changes to the site, 
work on the `website_and_docs` directory. To see a live preview of 
your changes, run `hugo server` on the site's root directory.

```shell
% git submodule update --init --recursive
% cd website_and_docs
% npm install
% hugo server
```

#### 标题大写

应该避免标题完全大写, 例如 _A Very Fine Heading_, 
应该书写为 _A very fine heading_ .
没有意义的大写字母或者无视拼写协议的标题, 通常会带来误解.
我们更倾向于使用句子首字母大写的 _sentence case_ 的方式.

#### 行的长度

在编辑以plain HTML格式编写的文档来源时, 请将行的长度限制在72个字符以内.

部分先进的贡献者, 使用了
[_semantic linefeeds_](//rhodesmill.org/brandon/2012/one-sentence-per-line),
这是一种不以HTML源码换行为基础的技术, 通过这种技术, 
公众看到的内容将会在文章中以“自然断开”的方式进行分割.
换句话说, 句子之间在更符合语义的地方被分割.
不必多虑每个段落的行, 强迫它们都以明确的边距结尾, 
而是可以将换行符添加到语义有断开的任何地方. 
(译者注：具体区别，对比本网页与原始md后，即可了解本段想表达的意思) 

通过git进行协作时, 
这种技术会使提交的差异更显而易见, 
但这不是我们强制贡献者使用的内容.

#### Translations

本文档基于英语内容, 被翻译成多种语言. 
更改文件时, 请 **确保** 也对所有其他翻译文件进行更改. 
这可能会略有不同, 例如:
 
* 如果将代码示例添加到 `browser_manipulation.en.md` 文件中后, 
则还需将其添加到 `browser_manipulation.es.md`, 
`browser_manipulation.ef.md`, 
`browser_manipulation.ja.md` 以及所有其他的已翻译文件.

* 如果您发现可以改进的翻译, 请仅更改翻译的文件. 

* 如果要添加新的语言翻译, 请添加具有适当后缀的新文件. 
无需翻译所有内容即可提交PR, 可以迭代完成. 
不要忘记在 `config.toml` 文件中检查一些必要的配置. 

* 如果您用英语版本更改了文本, 
请用您的更改替换翻译文件中的同一部分(是的, 用英语), 
然后在文件顶部添加以下注意事项. 

```
{{%/* pageinfo color="warning" */%}}
<p class="lead">
   <i class="fas fa-language display-4"></i> 
   Page being translated from 
   English to {LANGUAGE}. Do you speak {LANGUAGE}? Help us to translate
   it by sending us pull requests!
</p>
{{%/* /pageinfo */%}}
```

### 步骤 4: 提交

首先确保git知道您的姓名和电子邮件地址:

```shell
% git config --global user.name 'Santa Claus'
% git config --global user.email 'santa@example.com'
```

**编写良好的提交信息很重要.** 
提交信息应描述更改的内容, 
原因以及已解决的参考问题(如果有). 
撰写时应遵循以下规则:

1. 第一行应少于或等于50个字符, 并包含对该更改的简短说明.
2. 保持第二行空白.
3. 在所有72列处换行.
4. 包括 `Fixes #N`, 其中 _N_ 是提交修复的问题编号(如果有).

一个好的提交信息可能看起来像这样:

```text
explain commit normatively in one line

Body of commit message is a few lines of text, explaining things
in more detail, possibly giving some background about the issue
being fixed, etc.

The body of the commit message can be several paragraphs, and
please do proper word-wrap and keep columns shorter than about
72 characters or so. That way `git log` will show things
nicely even when it is indented.

Fixes #141
```

第一行必须有意义, 因为这是人们在运行 `git shortlog` 或 `git log --oneline` 时看到的内容.

### 步骤 5: Rebase

使用 `git rebase` (并非 `git merge`) 同步实时的工作.

```shell
% git fetch upstream
% git rebase upstream/trunk
```

### 步骤 6: 测试

永远记住要[运行本地服务](https://gohugo.io/getting-started/usage/#livereload), 
这样做可以确保您的更改没有破坏任何事情. 

### 步骤 7: Push

```shell
% git push origin my-feature-branch
```

访问 https://github.com/yourusername/seleniumhq.github.io.git
并点击 _Pull Request_ 以及填写表格.
 **请明确您已经签署了CLA** (详见步骤 7).

Pull requests通常会在几天内进行审核. 
如果有评论要解决, 请在新提交(最好是[修正](http://git-scm.com/docs/git-commit))中应用您的更改, 
然后推push到同一分支.

### 步骤 8: 集成

代码审查完成后, 提交者将获取您的PR并将其集成到项目的trunk分支中. 
因为我们希望在trunk分支上保持线性历史记录, 
所以我们通常会squash并rebase您的分支历史记录.

## 沟通

有关如何与项目贡献者和整个社区进行沟通的所有详细信息, 
请访问以下网址 https://selenium.dev/support
