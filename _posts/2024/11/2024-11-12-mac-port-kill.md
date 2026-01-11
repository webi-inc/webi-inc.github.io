---
title: "포트 충돌 해결: Port 80 was already in use (lsof, kill)"
description: "개발 중 발생하는 'Port 80 was already in use' 오류 해결 방법.터미널에서 lsof 명령어로 포트를 점유 중인 프로세스(PID)를 찾고, kill 명령어로 강제 종료하여 포트 충돌을 해결하는 과정을 단계별로 정리했습니다."
date: 2024-11-12 10:28:16 +0900
categories: [Linux, Terminal]
tags: [port, lsof, kill, error, terminal]
image:
  path: "/assets/img/posts/mac-port-kill/list.jpeg"
  alt: "Photo by Lewis Kang'ethe Ngugi / Unsplash"
published: true
---

개발을 하다 보면 간혹 보이는 오류 문구  
"Port 80 was already in use."

해당 포트가 이미 사용중일 때 나타나는 오류 입니다.  
포트가 이미 사용중 일 때 찾아서 강제로 Kill하는 방법을 알아보겠습니다.

1. 포트 검색
```shell
lsof -i :80
```
검색하고자 하는 포트를 뒤에 적어줍니다. 저는 80포트로 검색을 했습니다.

2. 검색된 리스트 확인
```shell
COMMAND   PID   USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
java    33258     pc  125u  IPv6 0xb4fba925528e7965      0t0  TCP \*:http (LISTEN)
```
80포트를 사용 중인 리스트가 확인 되며, 리스트 중에 PID를 확인 해주세요.

3. 포트 Kill
```shell
kill -9 33258
```
이전에 리스트에서 확인한 PID를 이용하여 프로세스를 Kill 합니다.  

위와 같은 방법으로 포트를 죽인 후에 해당 포트를 사용하려는 작업을 재실행 할 경우 정상적으로 실행이 되는 것을 확인 하실 수 있습니다.
