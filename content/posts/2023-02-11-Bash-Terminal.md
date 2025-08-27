---
title:  "Bash Terminal 정리"
author: "Woohyuk Jang"
draft: false

date: "2023-02-11"
description: ""
categories:
  - cs/unix
tags:
  - Blog
---
### Bash Terminal 정리



이 글에서는 GNU Bash에서 자주 쓰이는 명령어들을 용도별로 정리한다.



1. 도움



* man \[command]: *manual*. 매뉴얼 표시.

* 보통 --help로 도움을 얻을 수 있다.



2\. 파일 트리 탐색



* pwd: *print working directory*. 현재 폴더 출력

* cd \[경로]: *change directory*. 주어진 경로로 이동. \~는 홈, ../..는 부모의 부모.

* ls: *list*. 현재 폴더 내 파일 출력



​ ​ ​​​ ​ ​​​ ​ ​​​ ​-R: *recursive*. 폴더 안 모든 파일을 출력



​ ​ ​​​ ​ ​​​ ​ ​​​ ​-a: *all*. 숨겨진 파일도 출력



​ ​ ​​​ ​ ​​​ ​ ​​​ ​-lh: *long human-readable*. -l은 파일의 권한, 소유 유저/그룹, 파일 크기, ​ ​ ​​​ ​ ​​​ ​ ​​​ ​수정 시각을 보여줌. -h는 파일 크기를 5MB처럼 인간이 읽기 쉽게 표시.



* find \<startingdirectory> \<options> \<search term>: starting directory에서 파일 찾기.



​ ​ ​​​ ​ ​​​ ​ ​​​-name: 이름으로 찾기. -iname은 대/소문자 무시.



​ ​ ​​​ ​ ​​​ ​ ​​​-type: 파일 종류로 찾기. search term으로 d(directory), f(file), l(symbolic ​ ​ ​​​ ​ ​​​ ​ ​​​link)등을 사용 가능.



3\. 파일 생성/삭제/복사/이동



* touch \[file]: file 생성

* mkdir \[dir]: *make directory.* 디렉토리 생성

* cp \[files] \[destination]: *copy*. destination에 파일 복사.



​ ​ ​​​ ​ ​​​ ​-R: *recursive*. 디렉토리 복사할 때.



* mv \[files] \[destination]: *move*. 파일 이동. 이름 바꿀 때도 사용.

* rm \[file]: *remove*. 파일 제거.



​ ​ ​​​ ​ ​​​ ​ -r: *recursive*. 디렉토리 제거할 때. 빈 디렉토리는 rmdir (*remove directory*)로 제거.



4\. 파일 조회



* cat \[file]: *concatenate*. 파일의 내용을 stdout에 더한다. (파일 내용 출력)

* grep \[re] \[file]: *global regular expression print*. 파일 내용 중 re match가 되는 행을 출력.

* head -n \[file]: 파일의 앞 n행 출력. 기본값 n=10.

* tail -n \[file]: 파일의 뒤 n행 출력. 기본값 n=10.

* diff \[file1] \[file2]: *difference*. 두 파일에서 차이나는 부분 출력.

* nano \[file]: nano editor로 파일 열기. nano editor에서 Ctrl+O는 파일 저장, Ctrl+X는 exit이다.



5\. 유저, 그룹 관리



리눅스에서는 여러 유저가 있다. 이들은 그룹을 가진다. 유저의 primary group은 유저에 의해 생성된 파일에 부여되는 그룹이다. 유저는 그 외 여러 secondary group에 가입될 수 있다.



* /etc/passwd: 사용자 정보를 담은 파일. (과거에 비밀번호를 이 파일에 저장해서 *password*)

* /etc/group: 그룹 정보를 담은 파일.

* whoami: 현재 유저명.

* id \[user]: 유저의 uid (user id), gid (group id), group를 출력. user의 기본값은 현재 유저.

* useradd \[user]: 유저 추가.

* userdel \[user]: 유저 삭제.

* su \[user]: *switch user*. 유저 변경.



6\. 권한 관리



* sudo (command):*&#x20;superuser do*. 관리자 권한으로 command 실행.

* chmod \[permission] \[file]: *change mode*. 파일의 권한을 바꾼다.



​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​ ​- 리눅스에서 권한은 r=4 (read), w=2 (write), x=1 (execute) 여부가 있으​ ​ ​​​ ​ ​​​ ​ ​ ​​​ ​ ​​​ ​​며, 파일 유저, 파일 그룹, other가 있다. 예)



​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​ ​rwxr-x — x 또는 751: 파일 유저는 read, write, execute. 파일 그룹은 ​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​ ​read, execute. 다른 유저들은 execute만 할 수 있다.



* chown \[user/group] \[file]: *change owner.&#x20;*&#xD30C;일의 소유권을 바꾼다.



7\. 인터넷 관련



* ping \[host]: host에 접속할 수 있는지, 시간은 얼마나 걸리는지 확인.

* wget \[webpage]: 웹페이지를 다운로드.

* hostname: 시스템 이름. -i 로 ip 주소를 알 수 있다.



8\. 시스템 관련



* df -h: *disk free human-readable*. 각 디스크별로 메모리가 얼마나 있는지 파악할 수 있다.

* du \[path] -h: *disk usage human-readable*. 폴더 아래 파일들의 디스크 사용량을 보여준다. -sh는 총량을 보여준다.

* jobs \[jobID] -l: jobID에 해당하는 job를 보여준다. -l 옵션은 list. jobID가 주어지지 않으면 현재 실행되는 job들을 보여준다.

* kill \[옵션] \[pID]: pID에 해당하는 process를 멈추게 한다.



​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​-SIGTERM: 프로세스의 정상적 종료



​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​-SIGKILL: 프로세스의 강제 종료



* top: *a top users display for Unix*. 프로세스가 자원(CPU, Memory)를 어떻게 사용하는지 보여준다.

* htop: *Hisham’s top*. Hisham이라는 사람이 만든 top. 발전된 반응형 top.

* ps: *process status*. 현재 실행중인 프로세스의 PID (process id), TIME (실행시간), CMD (command) 등을 보여준다.



9\. 기타



* history: 지금까지 실행한 linux command를 보여준다.

* alias name=string: 말 그대로 별명을 만든다.

* unalias name: 별명 삭제

* apt-get (commands): *advanced package tool*. 패키지 관리용.



​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​- update, upgrade, check 등이 있다.



* zip \[zipfile] \[파일들]: zip 파일을 만든다.

* unzip \[zipfile]: zip을 푼다.

* tar:*&#x20;tape archive*. 아카이빙 (파일을 묶어서 사본을 만듬).



​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​tar -cf \[archive\_file] \[to\_be\_archived]: *create (tar file from) filename*.



​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​tar -xf \[archive\_file]: *extract (tar file named) filename*.



​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​중간에 -czf와 같이 file compression method를 추가할 수 있다.



​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​-z: gzip, -j: bz2.



10\. 유용한 연습 사이트/더 깊이 파고 싶다면…



[https://cmdchallenge.com/](https://cmdchallenge.com/#/create_file)



[**GitHub - ibraheemdev/modern-unix: A collection of modern/faster/saner alternatives to common unix…**\

*A cat clone with syntax highlighting and Git integration. A modern replacement for ls. The next gen file listing…*&#x67;ithub.com](https://github.com/ibraheemdev/modern-unix "https://github.com/ibraheemdev/modern-unix")[](https://github.com/ibraheemdev/modern-unix)



<https://www.learnenough.com/command-line-tutorial>



11\. 출처



<https://www.hostinger.com/tutorials/linux-commands>



​ ​ ​​​ ​ ​​​ ​​ ​ ​​​ ​ ​​​



By [Woohyuk Jang](https://medium.com/@morrranii) on [February 11, 2023](https://medium.com/p/e31c993c7f8e).

Exported from [Medium](https://medium.com) on August 26, 2025.
