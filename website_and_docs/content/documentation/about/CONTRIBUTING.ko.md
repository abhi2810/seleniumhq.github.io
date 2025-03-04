---
title: "Selenium 사이트와 문서에 기여하기"
linkTitle: "Selenium 사이트와 문서에 기여하기"
weight: 2
aliases: 
        [
          "/documentation/ko/contributing/",
          "/documentation/ko/front_matter/typographical_conventions/"
        ]
---

{{% pageinfo color="warning" %}}
<p class="lead">
   <i class="fas fa-language display-4"></i> 
   Page being translated from 
   English to Korean. Do you speak Korean? Help us to translate
   it by sending us pull requests!
</p>
{{% /pageinfo %}}

Selenium은 거대한 소프트웨어 프로젝트로, 사이트와 문서는 작동 원리를 이해하고 잠재력을 효과적으로 활용하는 데 중요한 역할을 합니다.

이 프로젝트는 Selenium 사이트와 문서를 담고 있습니다.
여기엔 Selenium을 효과적으로 사용하기 위한 업데이트 정보를 제공하고, 어떻게 참여하고 기여할 수 있는지에 대한 지속적인 노력이 모여 있습니다.

사이트와 문서에 기여하기 위한 방법은 아래 기술된 과정을 따릅니다. 여러분은 익숙해질 때 까지

---

Selenium은 여러분의 기여를 환영합니다. 기여하는 방법은 여러 가지가 있습니다:

## 이슈 제기하기

새로운 이슈를 제기하거나 기존 이슈에 코멘트를 남길 때, 논의 내용이 Selenium 소프트웨어, 사이트 또는 문서의 구체적인 기술적인 문제와 관련이 있는지 확인해주시기 바랍니다.

Selenium의 모든 구성요소는 빠르게 변하기 때문에, 문서 내용이 업데이트 이전의 내용일 수도 있습니다.
이런 경우를 발견하신다면, 주저하지 마시고 이슈를 제기해주시기 바랍니다.
문서 내용을 직접 최신화하실 수 있다면, 변경 내용에 대한 pull request를 해주시기 바랍니다.

만약 여러분이 발견한 것이 이슈인지 아닌지 헷갈리신다면,
다음의 커뮤니케이션 채널을 통해 질문해주시기 바랍니다.
https://selenium.dev/support.

## 기여하기

Selenium 프로젝트는 새로운 기여자를 환영합니다. 꾸준히 중요하고 가치가 높은 기여를 해주신 기여자는 _Committers_ 가 되어 프로젝트에 커밋 접근 권한을 갖게 됩니다.

아래 가이드는 여러분에게 기여하는 과정을 안내합니다.

### 1 단계: Fork

프로젝트를 [Github](https://github.com/seleniumhq/seleniumhq.github.io) 에서 Fork 하시고,
로컬에 복사되었는지 확인하세요.

```shell
% git clone git@github.com:seleniumhq/seleniumhq.github.io.git
% cd seleniumhq.github.io
```

#### 의존성: Hugo

We use [Hugo](https://gohugo.io/) and the [Docsy theme](https://www.docsy.dev/)
to build and render the site. You will need the “extended” 
Sass/SCSS version of the Hugo binary to work on this site. We recommend
to use Hugo 0.83.1 or higher.

Please follow the [Install Hugo](https://www.docsy.dev/docs/getting-started/#install-hugo) 
instructions from Docsy.

### 2 단계: Branch

기능을 추가한 branch를 생성하고 개발을 시작하세요:

```shell
% git checkout -b my-feature-branch
```

우리는 HEAD-based development 지향하고 있으며, 모든 변경사항은 trunk에 바로 적용됩니다.

### 3 단계: Make changes

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
#### Capitalisation of titles

One should avoid title capitalisation,
such as _A Very Fine Heading_,
and instead go for _A very fine heading_.
Gratuitous capitalisation, or title case,
often show a misunderstanding of – or a disregard for –
orthographic conventions.
We prefer what is known as _sentence case_,
with a single initial capital to start headers.

#### Line length

When editing the documentation’s source,
which is written in plain HTML,
limit your line lengths to around 72 characters.

Some of us take this one step further
and use what is called
[_semantic linefeeds_](//rhodesmill.org/brandon/2012/one-sentence-per-line),
which is a technique whereby the HTML source lines,
which are not read by the public,
are split at ‘natural breaks’ in the prose.
In other words, sentences are split
at natural breaks between clauses.
Instead of fussing with the lines of each paragraph
so that they all end near the right margin,
linefeeds can be added anywhere
that there is a break between ideas.

This can make diffs very easy to read
when collaborating through git,
but it is not something we enforce contributors to use.

#### Translations

문서는 다양한 언어로 번역되어 있으며, 번역은 영문에 기반을 두고 있습니다.
문서를 변경할 때는, 다른 모든 번역 문서도 변경해야 하는 점을 **반드시 유의** 해주시기 바랍니다.
이는 어떤 부분을 변경하느냐에 따라 달라질 수 있습니다, 예를 들어:
 
* 만약 여러분이 `browser_manipulation.en.md` 파일에 코드 예제를 추가했다면,
`browser_manipulation.es.md`, `browser_manipulation.ef.md`, 
`browser_manipulation.ja.md`, 그리고 다른 모든 번역 문서에도 추가해주셔야 합니다.
* 만약 여러분이 번역 문서의 개선사항을 발견했다면,
해당 번역 문서만 변경하시면 됩니다.
* 만약 여러분이 새로운 언어의 번역을 추가하고자 한다면, 알맞은 접미사 파일명의 문서를 추가해주셔야 합니다. PR을 할 때, 모든 문서가 번역되어있을 필요는 없습니다, 번역은 때마다 반복적으로 하셔도 됩니다. `config.toml` 파일에 필요한 설정값을 잊지 마시고 확인해주시기 바랍니다.
* 만약 여러분이 영문 문서에 내용을 바꿨다면, 다른 번역 문서의 같은 부분에 변경된 내용(영어로)을 넣어주시기고, 문서의 최상단부에 아래와 같은 알림을 추가해주시기 바랍니다.


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

### 4 단계: Commit

먼저 git에 이름과 이메일 주소를 입력하시기 바랍니다:

```shell
% git config --global user.name 'Santa Claus'
% git config --global user.email 'santa@example.com'
```

**적절한 커밋 메시지를 쓰는 것이 중요합니다.** 커밋 메세지는
무엇이, 왜 변경되었는지 설명해야 하며, 수정된 이슈들을 언급해야 합니다(만약에 있다면).
작성할 때 이 가이드라인들을 따르시기 바랍니다.

1. 첫 줄은 50자 내외 혹은 그 이하이어야 하며 변경 사항의 짧은 설명을 포함해야 합니다.  
2. 두 번째 줄은 공백으로 두시기 바랍니다. 
3. 다른 모든 줄은 72자 내로 작성하십시오. 
4. _N_ 이 수정사항을 커밋한 이슈 번호인, `Fixes #N`을 포함하십시오.  


좋은 커밋 메세지는 이렇습니다:

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

첫 줄은 사람들이 `git shortlog` 나 `git log --oneline` 을 실행하면 보는 것이기 때문에 의미있어야합니다. 

### 5 단계 : Rebase

작업을 동기화하려면 `git rebase`를 사용하십시오. (`git merge`가 아니라)

```shell
% git fetch upstream
% git rebase upstream/trunk
```

### 6 단계: 테스트

항상 로컬 서버를 실행하는 것을 기억하십시오. 그러면 당신의 변경 사항들이 아무것도 안 건드리고 안전합니다. 

### 7 단계 : Push

```shell
% git push origin my-feature-branch
```

https://github.com/yourusername/seleniumhq.github.io.git 에서  _Pull Request_ 를 누르고 형식을 채우시기 바랍니다. **CLA에 서명했는지 나타내주시길 바랍니다** (7 단계 참고)

Pull request 는 몇 일 내에 확인됩니다. 주소에 코멘트들이 있다면, 새로운 커밋에 변경 사항(가급적
[fixups](http://git-scm.com/docs/git-commit))을 적용하고 같은 branch 에 push 해주시기 바랍니다. 

### 8 단계 : Integration

코드 확인이 완료되었으면, committer는 당신의 PR을 저장소의 trunk branch에 통합할 것입니다. 왜냐하면 우리는 trunk branch에 순차적인 이력을 유지하고 싶기 때문에, 우리는 당신의 branch 이력은 squash나 rebase 할 것입니다. 

## 커뮤니케이션


프로젝트 기여자들과 커뮤니티와 어떻게 소통할지에 대한 자세한 사항은 https://selenium.dev/support 에서 찾을 수 있습니다. 

