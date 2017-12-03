---
date: '2017-10-30 10:30'
title: '[Hexo로 포스팅하기 1] Hexo를 설치해 보자'
tags:
  - hexo
  - blog
categories:
  - hexo
published: true
---

<!--![](images/debug.gif)-->
[Hexo](https://hexo.io/)는 Node.js 기반의 static site 생성기이다. Hexo를 설치하고 Github에 호스팅하는 방법을 알아보려고 한다. 블로그 작성을 시작해야 겠다고 마음 먹은 후로 wordpress, tistory같은 php 기반툴들과 jekyll, hexo와 같은 static site 생성들 중에 어떤 것을 사용할 지 고민을 했었다. 그러다 나의 Geek스러움이 특이한 것에 이끌리게 했고, 개발자들이 블로그에 많이 사용하는 static site를 사용하기로 했다. 그 뒤에 jekyll을 사용하려고 했었지만, 테마를 찾다보니 Hexo의 icarus라는 테마가 마음에 들어 Hexo로 블로깅을 하기로 했다.

<!-- more -->

## Hexo 설치
Hexo를 설치하기 위해서는 Node.js가 필요하며, github 호스팅을 위해 git을 설치해야 한다. git 설치 및 사용을 위해서는 다음 사이트들을 참고하면 된다.
* [Git 홈페이지](https://git-scm.com/)
* [Git 간편 안내서](https://rogerdudler.github.io/git-guide/index.ko.html)

[Nodejs 공식 홈페이지](https://nodejs.org/ko/)에서 다운받을 수도 있지만, 버전 관리를 위해 [nvm](https://github.com/creationix/nvm)을 통한 설치를 추천한다.</br>
cURL을 이용하여 nvm 및 Node.js 설치
```bash
$ curl https://raw.github.com/creationix/nvm/master/install.sh | sh
$ nvm install stable
```
Node.js를 설치한 뒤 다음 명령어를 통해 hexo를 설치한다. -g 옵션은 터미널에서 hexo 명령어를 사용할 수 있게 해주므로 사용하는 것을 추천한다.
```bash
$ npm install -g hexo-cli
```
참고로 맥에서는 Xcode 설치 후 Command Line Tools를 설치하고나서 사용해야 한다.

폴더를 생성한 후, 해당 폴더에서 다음 명령어를 입력하면 초기화 및 확인이 가능하다.
```bash
$ hexo init
$ hexo server
```

브라우저를 통해 [localhost:4000](http://localhost:4000)에 들어가면 다음과 같은 화면을 볼 수 있다.</br>
![hexo 초기 화면](http://d.pr/i/18Xgq.png)


## Github를 통해 Hexo 호스팅하기
우선 Github에 로그인 한 뒤 새 repository를 생성한다.</br>
![새 repository 생성 1](http://d.pr/i/1cvRa+ "")
그 후 repository 이름을 입력해야 하는데 (자신의 github 아이디).github.io와 같은 형식으로 해야 한다. 예를 들어, 나의 아이디는 pocketeer이므로 pocketeer.github.io를 입력해 주면 된다. </br>
![새 repository 생성 2](http://d.pr/i/LmsY+ "")
repository 주소를 복사한다.</br>
![repository 주소 복사](http://d.pr/i/12qZK+ "")

이제 _config.yml에서 deploy에 아까 복사한 repository 주소를 넣으면 된다.
참고로 자세한 설명은 생략하겠지만 bitbucket의 repository 주소를 넣어도 가능하다.
```bash
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: [복사한 repository 주소]
  branch: master
```

꼭 할 필요는 없지만, 플러그인 연동시 문제가 될 수 있으므로 다음처럼 url도 바꿔주는 것이 좋다.
```yml
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://(자신의 github 아이디).github.io
```

github에서 자동으로 hexo 템플릿에 따라 사이트를 생성해 주지는 않기 때문에, github repository에 deploy하기 전에 다음 명령어를 입력하여 사이트를 생성해 주어야 한다. 생성된 사이트는 public 폴더에 있다.
```bash
$ hexo generate
```

그 후에 다음 명령어를 입력하면, _config.yml에 넣었던 repository에 public 폴더안의 파일들을 deploy해준다.
```bash
$ hexo deploy
```

보통 사이트를 업데이트하기 위해서는 앞의 두 명령어를 차례로 입력해야 하는데, 좀 귀찮다. 이를 위해 다음 두 명령어처럼 한번에 가능하다. 두 개다 사이트를 생성 후 deploy해준다.
```bash
$ hexo deploy -g    # g는 generate의 g
$ hexo generate -d  # d는 deploy의 d 
```

이제 확인을 위해 브라우저를 통해 http://(자신의 github 아이디).github.io에 들어가면 자신의 블로그를 확인할 수 있다.

## 끝으로
지금까지 Github를 통해 Hexo를 호스팅하는 방법에 대해 알아보았다. Hexo에 대해 계속해서 포스팅할 예정이지만, 정보를 더 얻고 싶으면 [Hexo의 문서](https://hexo.io/docs/)를 보는 것도 추천한다. 다음 글에서는 Hexo로 글쓰는 방법에 대해 알아본다.

## 참고링크
* [Hexo](https://hexo.io/)
* [Hexo documentation](https://hexo.io/docs/)
