---
title:  "Bash Terminal 정리2"
author: "Woohyuk Jang"
draft: false

date: "2023-02-12"
description: ""
categories:
  - cs/unix
tags:
  - Blog
---
### Bash Terminal 정리2



오늘은 [로드맵](https://roadmap.sh/backend)에 나와있는 terminal command를 정리해본다. [Bash Terminal 정리](https://medium.com/@morrranii/bash-terminal-%EC%A0%95%EB%A6%AC-e31c993c7f8e)에 있는 내용은 정리하지 않았다 (wget, head, tail). 다만 grep은 더 자세히 알아보기 위해 다시 정리한다.



1. awk: *Aho, Weinberger, and Kernighan*. (개발자 이름)



패턴 매칭, 처리로 잘 이용된다.



awk options ‘selection\_criteria {action}’ input\_file



* input file에서 selection\_criteria를 충족하는 행(record)들을 읽어 action을 취한다.

* awk ‘/target/ {print}’ example.txt는 파일에서 target을 찾아 출력한다.

* awk ‘{print $1}’ example.txt는 파일 각 줄에서 whitespace가 오기 전 내용을 출력한다. ($0은 전체 행, $1,$2 등은 whitespace로 구분된 각 field)

* awk는 NR (number of record), NF (number of field), FS (field separator) 등의 내장변수가 있다.



자세한 내용은 [여기](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)를 참고하자.



2\. sed: *stream editor*.



정규 표현식을 이용하여 find & replace하는 용도로 자주 사용된다.



sed options script input\_file



* sed ‘s/re/replace’ example.txt는 파일에서 대체 (s-*substitute*)한다. /로 구분되어 찾을 정규 표현식이 나오고, 역시 / 다음에 대체 문자열이 온다. 각 줄에서 첫번째 occurence만을 대체한다.

* sed ‘s/re/replace/n’ example.txt는 n번째 occurence를 대체한다.

* sed ‘s/re/replace/g’ example.txt는 모든 occurence를 대체 (g-*global*)

* sed ‘2,$ s/re/replace’ example.txt는 2번째부터 끝 행에서 대체한다.



자세한 내용은 [여기](https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/)를 참고하자.



3\. lsof: *list of open files*



무슨 프로세스가 무슨 파일을 열었는지 보여준다. unix-like system에서는 폴더, 링크 등등이 모두 파일임을 기억하자. 아래 소개할 grep과 함께 자주 사용한다.



lsof \[option] \[username]



* lsof는 열려있는 파일을 보여준다.

* lsof -u username은 특정 유저가 연 파일을 보여준다. username 앞에 not의 의미로 ^를 붙일 수 있다.

* lsof -c commandname은 특정 명령이 연 파일을 보여준다.

* lsof -p processID는 특정 프로세스가 연 파일을 보여준다.

* -R은 parent process ID를 같이 보여준다.

* -i는 네트워크 커넥션을 확인할 수 있다.



자세한 내용은 [여기](https://www.geeksforgeeks.org/lsof-command-in-linux-with-examples/)를 참고하자.



4\. grep: *global regular expression print.*



특정 regular expression 패턴에 맞는 행들을 찾아 출력한다.



grep \[options] pattern



* -c: *count*. 행의 개수만 출력.

* -i: *ignore*. 대소문자 무시

* -R: *recursive*. 디렉토리 내 행 찾기.

* -l: *list?* 파일 이름만 출력.

* -h: 매칭된 행만 출력



자세한 내용은 [여기](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)를 참고하자.



5\. curl: *client URL*.



HTTP, HTTPS, FTP, IMAP 등의 프로토콜을 이용하여 정보를 주고 받는다. 유저 반응 없이 동작하여 자동화에 좋다고 한다.



curl \[options] \[url]



* curl <https://google.com:> 주소에 접속한다.

* 여러 프로토콜에 접속할 수 있다. 나는 이 프로토콜들에 대해 잘 모르기 때문에 더 정리하지 않을 것이다. 자세한 내용은 [여기](https://www.geeksforgeeks.org/curl-command-in-linux-with-examples/)를 참고하자.



6\. less: 말 그대로 적다는 의미이다. 한 페이지만 일단 로딩한다. 크기가 큰 파일을 빨리 읽을 때 도움이 된다. 방향키로 스크롤하고 q로 나가자.



less filename



* -p: *pattern*. 특정 패턴이 처음으로 매칭되는 지점부터 시작하라.



7\. ssh: *Secure Shell*.



원격 서버/시스템 조절에 사용된다. 데이터가 암호화되므로 안전(secure)하다. TCP/IP port 22에서 작동한다. 로그인 후에는 그냥 원격 컴퓨터의 터미널을 사용한다고 생각하면 된다.



ssh username\&host



* ssh-keygen을 사용하면 공개키를 만들 수 있다.

* -p: *port number*.



자세한 내용은 [여기](https://www.geeksforgeeks.org/ssh-command-in-linux-with-examples/)를 참고하자.



8\. dig: *Domain Information Groper.*



nslookup의 발전된 버전이다.



dig \[server] \[name] \[type]



* A, ANY, MX와 같이 레코드 타입을 설정할 수 있다. 기본값은 A.

* +short (IP 주소만 표시), +answer (레코드 전체 표시), +stats와 같이 추가 정보를 표시/생략할 수 있다.

* +trace에서는 dig가 직접 IP 주소를 네임서버들에 물어 찾고 그 과정을 보여준다.

* @serverip와 같이 찾을 서버를 설정할 수 있다.

* 예시:



```

dig google.com ANY @8.8.8.8 +answer

```



자세한 내용은 [여기](https://www.geeksforgeeks.org/dig-command-in-linux-with-examples/)를 참고하자.



9\. 참고 자료/더 깊이 파보려면…



[**AWK command in Unix/Linux with examples - GeeksforGeeks**\

*Awk is a scripting language used for manipulating data and generating reports. The awk command programming language…*&#x77;ww.geeksforgeeks.org](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/ "https://www.geeksforgeeks.org/awk-command-unixlinux-examples/")[](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)



[**Sed Command in Linux/Unix with examples - GeeksforGeeks**\

*SED command in UNIX stands for stream editor and it can perform lots of functions on file like searching, find and…*&#x77;ww.geeksforgeeks.org](https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/ "https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/")[](https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/)



[**lsof command in Linux with Examples - GeeksforGeeks**\

*Linux/Unix consider everything as file and maintains folder. So "Files or a File " is very important in Linux/Unix…*&#x77;ww.geeksforgeeks.org](https://www.geeksforgeeks.org/lsof-command-in-linux-with-examples/ "https://www.geeksforgeeks.org/lsof-command-in-linux-with-examples/")[](https://www.geeksforgeeks.org/lsof-command-in-linux-with-examples/)



[**grep command in Unix/Linux - GeeksforGeeks**\

*The grep filter searches a file for a particular pattern of characters, and displays all lines that contain that…*&#x77;ww.geeksforgeeks.org](https://www.geeksforgeeks.org/grep-command-in-unixlinux/ "https://www.geeksforgeeks.org/grep-command-in-unixlinux/")[](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)



[**curl command in Linux with Examples - GeeksforGeeks**\

*is a command-line tool to transfer data to or from a server, using any of the supported protocols (HTTP, FTP, IMAP…*&#x77;ww.geeksforgeeks.org](https://www.geeksforgeeks.org/curl-command-in-linux-with-examples/ "https://www.geeksforgeeks.org/curl-command-in-linux-with-examples/")[](https://www.geeksforgeeks.org/curl-command-in-linux-with-examples/)



[**less command in Linux with Examples - GeeksforGeeks**\

*Less command is a Linux utility that can be used to read the contents of a text file one page(one screen) at a time. It…*&#x77;ww.geeksforgeeks.org](https://www.geeksforgeeks.org/less-command-linux-examples/ "https://www.geeksforgeeks.org/less-command-linux-examples/")[](https://www.geeksforgeeks.org/less-command-linux-examples/)



[**ssh command in Linux with Examples - GeeksforGeeks**\

*ssh stands for "Secure Shell". It is a protocol used to securely connect to a remote server/system. ssh is secure in…*&#x77;ww.geeksforgeeks.org](https://www.geeksforgeeks.org/ssh-command-in-linux-with-examples/ "https://www.geeksforgeeks.org/ssh-command-in-linux-with-examples/")[](https://www.geeksforgeeks.org/ssh-command-in-linux-with-examples/)



[**dig Command in Linux with Examples - GeeksforGeeks**\

*dig command stands for Domain Information Groper . It is used for retrieving information about DNS name servers. It is…*&#x77;ww.geeksforgeeks.org](https://www.geeksforgeeks.org/dig-command-in-linux-with-examples/ "https://www.geeksforgeeks.org/dig-command-in-linux-with-examples/")[](https://www.geeksforgeeks.org/dig-command-in-linux-with-examples/)



By [Woohyuk Jang](https://medium.com/@morrranii) on [February 12, 2023](https://medium.com/p/b125ce19be50).

Exported from [Medium](https://medium.com) on August 26, 2025.
