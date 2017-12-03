---
title: (Hexo로 포스팅하기 2) Hexo로 글쓰기
tags:
  - hexo
  - blog
categories:
  - hexo
date: '2017-09-22 01:44 +0900'
published: false
---
## 포스팅하기

## 초안(draft) 작성
포스팅을 할 때 글을 조금씩 완성해나가면서 포스팅이 마음에 들 때 다른 사람들이 봐주길 원할 것이다. Hexo에서는 발행하기 이전 단계로 초안(draft)를 작성 할 수 있다.</br>
초안을 작성하는 법은 간단하다. 다음 명령어를 입력하면 된다.
```bash
$ hexo new draft <title>
```
이 명령어를 입력하면 source/_draft 폴더를 생성하여 해당 초안을 생성해 준다.
![생성된 초안](http://d.pr/i/1kbMP+)
초안을 블로그에서 확인하기 위해서는 다음처럼 draft 옵션을 추가해주면 된다.
```bash
$ hexo server --draft
```