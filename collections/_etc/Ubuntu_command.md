---
title: Ubuntu 명령어 관련
author: Joonseo Hyeon
layout: post
---

개인적으로 자주 사용했었던 Ubuntu 명령어 정리
기본적으로 관리자 권한을 얻기 위해서는 sudo를 앞에 붙이며 비밀번호를 요구함

## GPU 확인

nividia-smi

## 하드 용량 확인

df -h

- 하드디스크 단의 용량 확인

du -sh -a 디렉토리명/*

- 해당 디렉토리의 모든 폴더와 파일(-a)의 용량을 읽기 쉽게(-sh) 출력

## 백그라운드 실행(screen 계열 명령어)

### screen 바깥에서

screen -S 이름

- 데몬 등이랑은 좀 다른 듯? 백그라운드에 이름으로 명명된 프로세스를 생성해서 실행

screen -ls

- 현재 실행중인 screen 확인

screen -r 이름

- 이름으로 지정된 screen에 재진입

screen -S 이름 -X kill

- 이름으로 지정된 screen을 종료
- 이 명령어를 사용하지 않고 프로세스 id를 직접 kill하는 경우 좀비 프로세스가 되므로 주의

### screen 내부에서

ctrl+a d

- 실행 중인 상태로 현재 창 빠져나오기

ctrl+a k

- 실행을 종료하면서 현재 창 빠져나오기

## 프로세스

ps -ef

- 실행중인 프로세스 전체 목록 출력

kill -9 프로세스 id

- 프로세스 id에 해당하는 프로세스 종료
- **시스템 프로세스를 종료시키는 경우 문제가 발생하므로 항상 종료하기 전에 재확인**

## 파일 관련

cd ..

- 상위 폴더로 이동

cd 디렉토리명

- 해당 디렉토리로 이동

ls -a

- 현재 디렉토리 기준 모든 폴더를 출력 (-a를 사용하면 숨겨진 폴더까지 포함)

rm -r -f 디렉토리명

- 디렉토리명 아래의 모든 폴더와 파일을(-r) 강제적으로 (-f) 삭제
- **절대 복구가 안되므로 사용시 매우 주의를 요함! 시스템을 실수로 날리는 경우 부팅 불가능!**

## SSH 관련

systemctl status sshd

- ssh 서비스 실행 확인, active (running)일 경우 현재 서버가 열려있음

ss -nlt

- listem 상태인 ip-port 목록
- ssh 접속을 허용하는 port 번호가 listen 상태로 등록되어야 함

ufw enable/disable

- 방화벽 활성화/비활성화

ufw status verbose

- 허용된 방화벽 포트번호 확인

ufw allow 포트번호

- 해당 포트번호로의 통신 허용

ssh 아이디@ip주소 -p 포트번호

- ip주소에 해당하는 서버에 아이디에 해당하는 사용자 계정으로 포트번호를 통해 로그인
- windows의 ssh 통신도 같은 명령어 사용