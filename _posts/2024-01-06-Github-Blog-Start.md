---
title: Github 블로그 시작
date: 2024-01-06 17:16:00 +0900
categories: [Github Blog]
tags: [Github Blog]     # TAG names should always be lowercase
---

## Github 블로그 시작 

안녕하세요. Winey 입니다.<br>
블로그 첫 포스트에서 Github 블로그를 만들면서 들었던 생각과 블로그를 배포하는 과정에서 발생했던 문제를 공유해보겠습니다.<br>
제가 사용하고 있는 블로그 테마는 [jekyll chirpy theme(v6.3.1)](https://github.com/cotes2020/jekyll-theme-chirpy) 입니다.<br>
<br>

---

## Github 블로그 배포

깃 블로그를 배포하면서 다른 포스트들도 많이 참고 하였고 배포하면서 느낀 것을 공유해보자 합니다. <br>
<br>

### Github 블로그 배포 순서

보통 다른 Post에서 다루는 내용을 보면 아래의 순서로 이루어집니다.<br>
1. Github ID 준비 
2. Ruby && Jekyll 
3. Jekyll Theme 적용 
<br>

순서를 약간 바꿔 아래 처럼 준비하는게 좀 더 초기 오류를 덜 발생 시키지 않을까 생각합니다.<br>
1. Github ID 준비 
2. Github Theme 설정 
3. Ruby && Jekyll 설치
<br>

2,3 순서를 변경한 이유는 Jekyll Theme에서 Setup Ruby 버전이 명시 되어있다는 점 입니다.<br>
명시된 버전을 동일하게 사용하는 것이 조금이라도 오류를 줄이는 방법이 아닐까 생각합니다.<br>
제가 사용하고 있는 chirpy theme (v6.3.1)의 내용을 기준으로 아래와 같이 명시 되어 있습니다.<br>

```yaml
# {my_blog_local_repo}/.github/workflows/pages-deploy.yml
- name: Setup Ruby
  uses: ruby/setup-ruby@v1
  with:
    ruby-version: "3.2"
```
다른 jekyll theme의 Repository도 확인해보니 동일한 경로에 배포를 위한 yml이 있으니 해당 yml 파일을 참고하시면 될 것 같습니다.<br>
<br>

---

## Github 블로그 배포 실패 해결 사례

`Linux`  `MacOS` 환경에서는 초기 세팅을 위한 Script를 제공 하지만 `Windows` 환경에서 초기 세팅 시 수동으로 설정 해줘야 합니다.<br>
수동으로 설정 하는 만큼 저 역시 문제가 발생 하였고, 해당 문제를 해결 하는 과정을 공유 해보려고 합니다.<br>
<br>

### `/assets/js/dist/xxx.min.js  does not exit` 오류 문제

```
* At _site/xxx.html:1:

   internal script reference /assets/js/dist/commons.min.js does not exit 
```
오류의 내용은 `{my_repo}/assets/js/dist/commons.min.js` 파일을 찾지 못했다는 오류입니다. <br>
<br>
아무래도 제가 초기 설정 과정에서 누락한 것이 있는 것 같아 `tools/init` script 내용을 다시 살펴 봅시다. <br>

```bash
# {my_local_repo}/tools/init 

init_files() {
  if $_no_gh; then
    rm -rf .github
  else
    ## Change the files of `.github`
    mv .github/workflows/$ACTIONS_WORKFLOW.hook .
    rm -rf .github
    mkdir -p .github/workflows
    mv ./${ACTIONS_WORKFLOW}.hook .github/workflows/${ACTIONS_WORKFLOW}

    ## Cleanup image settings in site config
    _sedi "s/^img_cdn:.*/img_cdn:/;s/^avatar:.*/avatar:/" _config.yml
  fi

  # remove the other files
  rm -rf _posts/*

  # build assets
  npm i && npm run build

  # track the js output
  _sedi "/^assets.*\/dist/d" .gitignore
}
```

아래의 명령어를 입력하는 것을 놓치고 말았네요 ㅠㅠ <br>

```bash
  # build assets
  npm i && npm run build
```

위 명령어를 하나씩 수행해 봅시다.<br>

```bash
# npm install 수행 
winey-dev.github.io> npm install

npm WARN deprecated @babel/plugin-proposal-class-properties@7.18.6: This proposal has been merged to the ECMAScript standard and thus this plugin is no longer maintained. Please use @babel/plugin-transform-class-properties instead.

added 356 packages, and audited 357 packages in 18s

48 packages are looking for funding
  run `npm fund` for details
```

```bash
# npm run build 수행
winey-dev.github.io> npm run build

> jekyll-theme-chirpy@6.3.1 prebuild
> npx rimraf assets/js/dist


> jekyll-theme-chirpy@6.3.1 build
> NODE_ENV=production npx rollup -c --bundleConfigAsCjs

'NODE_ENV'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는
배치 파일이 아닙니다.
```

npm run build 수행 시 Error가 발생하는 것을 확인했으니 해당 Error를 해결 해보고 다시 명령어를 수행해 봅시다.<br>
> 해당 오류는 `npm install -g win-node-dev`를 수행하면 해결 됩니다. 

```bash
# npm install -g win-node-env 수행
winey-dev.github.io> npm install -g win-node-env

added 1 package in 943ms

# npm run build 수행
winey-dev.github.io> npm run build

> jekyll-theme-chirpy@6.3.1 prebuild
> npx rimraf assets/js/dist


> jekyll-theme-chirpy@6.3.1 build
> NODE_ENV=production npx rollup -c --bundleConfigAsCjs


_javascript/commons.js → assets/js/dist/commons.min.js...
created assets/js/dist/commons.min.js in 574ms

_javascript/home.js → assets/js/dist/home.min.js...
created assets/js/dist/home.min.js in 242ms

_javascript/categories.js → assets/js/dist/categories.min.js...
created assets/js/dist/categories.min.js in 217ms

_javascript/page.js → assets/js/dist/page.min.js...
created assets/js/dist/page.min.js in 222ms

_javascript/post.js → assets/js/dist/post.min.js...
created assets/js/dist/post.min.js in 220ms

_javascript/misc.js → assets/js/dist/misc.min.js...
created assets/js/dist/misc.min.js in 221ms
```

assets/js/dist에 파일들이 정상적으로 생성되었습니다.!!!<br>

---

## 마무리 
항상 어떤 블로그를 사용 할까 고민하기를 반복하다가 깃 블로그를 시작하게 되었습니다.<br>
글 재주가 없어 ... 이 글을 읽는 분들이 이해하기 어려울 수도 있지만 계속 블로그를 작성하다보면 제 글 실력도 올라가지 않을까요 ??
부디 그 날이 오기를 ㅠㅠ <br>
<br>
다음 포스트에서는 Chripy Theme를 커스터마이징 하는 방법에 대해서 다루어 볼까 합니다.<br> 
