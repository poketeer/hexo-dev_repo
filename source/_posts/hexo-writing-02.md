---
date: '2017-12-04 11:44 +0900'
title: (Hexo로 포스팅하기 2) Hexo로 글쓰기
tags:
  - hexo
categories:
  - hexo
published: true
thumbnail: 'https://cl.ly/102W1F2T0y3J/Image%202017-12-04%20at%203.33.04%20AM.png'
banner: 'https://cl.ly/102W1F2T0y3J/Image%202017-12-04%20at%203.33.04%20AM.png'
---
## 포스팅하기

## 초안(draft) 작성
포스팅을 할 때 글을 조금씩 완성해나가면서 포스팅이 마음에 들 때 다른 사람들이 봐주길 원할 것이다. Hexo에서는 발행하기 이전 단계로 초안(draft)를 작성 할 수 있다.</br>
초안을 작성하는 법은 간단하다. 다음 명령어를 입력하면 된다.
```bash
$ hexo new draft [title]
```
이 명령어를 입력하면 source/_draft 폴더를 생성하여 해당 초안을 생성해 준다.
초안을 블로그에서 확인하기 위해서는 다음처럼 draft 옵션을 추가해주면 된다.
```bash
$ hexo server --draft
```

_draft 폴더에 있던 파일을 _posts 폴더로 옮기기 위해 다음 명령어를 사용할 수 있다.
[title]에는 _draft 폴더에 있는 파일 이름을 입력하면 된다.
```bash
$ hexo publish [title]
```

## 마치며
hexo의 다른 명령어들을 알기 위해서는 [Hexo Commands](https://hexo.io/ko/docs/commands.html)를 참고하면 된다.
다음 포스팅에서는 netlify를 이용해서 무료로 블로그를 만드는 법에 대해서 알아본다.
