---
layout: post
title: 깃허브에 제킬 테마 적용하기
category: GIT
tags: [git, blog]
comments: true
---

# 제킬로 홈페이지 테마 적용하기

- 제킬은 개인, 프로젝트 또는 좆기 사이트를 위한 블로그 인식 정적 사이트 생성기입니다.
- 루비로 작성됬으며, MIT라이센스에 따라 배포됩니다.

### 1. 루비 설치하기
- [루비 다운로드 사이트](https://rubyinstaller.org/downloads/)에서 루비 인스톨러를 다운받습니다.
- 사이트에서 Ruby+Devkit 2.5.5-1 (x64)을 클릭하여 다운로드 한 후 Next만 누르며 디폴트로 설치합니다.
- 윈도우 검색창에서 `Start Command Prompt with Ruby`를 실행합니다.
- 프롬프트 상에서 `chcp 65001`를 실행합니다.
    - 인코딩을 부여하기 위한 명령어인데 실행하지 않을 경우 이후 진행하게 될 온갖 명령어에서 오류가 발생하므로 꼭 진행하여야 합니다.
- 잼파일에 번들러를 인스털합니다.

```
gem install jekyll jekyll-feed bundler github-pages tzinfo-data
```

> [gem파일](https://stackoverflow.com/questions/14072880/what-is-the-use-of-gemfile-in-rails) : 프로젝트에 포함되는 gem들의 리스트를 명시합니다.  
> [Ruby-Gem](https://www.ruby-lang.org/ko/libraries/) : 루비에 특화된 `apt-get` 비슷한 분산 패키지 시스템으로 라이브러리의 작성이나 공개, 설치를 도와주는 시스템입니다.  
> [bundler](http://gembundler.com/) : Gem Bundler은 gem을 설치하고 추적하는데 도움을 줍니다.  

### 2. 제킬 테마 적용하기
- 제킬테마 사이트는 아래를 참조했습니다. 저는 지킬 테마 중에 [clean-blog테마](http://jekyllthemes.org/themes/clean-blog/)를 홈페이지에 적용했습니다.
    - <https://github.com/topics/jekyll-theme>  
    - <http://jekyllthemes.org/>  
    - <https://jekyllthemes.io/free>  
    - <http://themes.jekyllrc.org/>


- 클린 블로그 테마의 설명에 나와있는 대로 진행하면 됩니다. 저는 여기서 이해가 안 됬던 부분의 설명을 덧붙였습니다.
    1. 루비 터미널창에서 경로를 지정한 후 `jekyll new my-site`를 입력합니다.
    2. my-site폴더를 에디터로 연 뒤에 `Gemfile`안에 테마를 `gem "jekyll-theme-clean-blog"`로 변경합니다.
    3. 터미널 창에서 `bundle install`명령어를 입력합니다.
    4. my-site폴더안에 `_config.yml`파일을 `theme: jekyll-theme-clean-blog`로 변경합니다.
    5. 터미널에서 `bundle exec jekyll serve`명령어를 입력합니다.

- 로컬 서버에서 돌려봅니다.
    - `TIP`은 `jekyll serve --watch`로 서버를 실행하면 에디터의 변경을 바로바로 인식할 수 있습니다.

### 3. github에 올리기
1. 깃허브에서 홈페이지 만듭니다.

2. 로컬 서버에서 만들었던 폴더를 깃허브에 올립니다.[참조](https://docs.github.com/en/github/importing-your-projects-to-github/adding-an-existing-project-to-github-using-the-command-line)

```
$ git init
$ git add .
$ git commit -m "First commit"
$ git remote add origin remote repository URL
$ git remote -v
$ git push origin master

```


# 참조
- [제킬 공식문서](https://jekyllrb.com/)
- [루비 설치과정](https://wikidocs.net/91460)


