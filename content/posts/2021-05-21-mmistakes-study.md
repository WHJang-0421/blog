---
title:  "minimal mistakes theme 정리"
author: "Woohyuk Jang"
draft: false

date: "2021-05-21"
description: "jekyll theme 인 minimal mistakes로 블로그 글쓰는 법 정리."
categories:
  - journal/blog_story
tags:
  - Blog
last_modified_at: 2022-04-30
---

## 앞으로의 블로그 작성법
1. 블로그 글 작성  
`_posts` 폴더에 `yyyy-mm-dd-title.md` 형식으로 저장
2. 로컬 컴퓨터에서 확인 (선택)   
`bundle exec jekyll serve`
3. 블로그 포스팅  
3-1) `Ctrl`+`Shift`+`` ` `` (VSCode에서 Terminal을 여는 단축키)    
3-2) `git add .`    
3-3) `git commit -m "commit message"`    
3-4) `git push -u origin master`    

## _config.yml 파일을 수정한 경우: 다시 빌드 필요
반드시 `bundle exec jekyll serve`를 실행해야 한다.

## 참고 자료
[SWDeveloper님의 Github Pages 블로그 따라하기 시리즈](https://devinlife.com/howto/)

## 수정 기록
** 2022.04.30 수정
- WSL2, 즉 Linux 환경에서 블로그를 사용하는 방법을 중심으로 정리했다.
- _config.yml 파일을 바꿨을 때 업데이트 방법을 추가했다.
