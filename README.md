 # 과제 목표
 - 절대 경로와 상대 경로의 차이를 예시를 들어 설명할 수 있다.
 - 파일 권한의 의미(r/w/x)와 755, 644 같은 표기가 어떤 규칙으로 해석되는지 설명할 수 있다.
 - 기존 Dockerfile을 기반으로 “커스텀 이미지”를 만들 수 있다.
 - 포트 매핑이 필요한 이유를 설명할 수 있다.
 - Docker 볼륨(영속 데이터)을 설명할 수 있다.
 - Git과 GitHub의 역할 차이(로컬 버전관리 vs 원격 협업 플랫폼)를 설명할 수 있다.

# 실행 환경
- OS : macOS 15.7.4 (24G517)
- 쉘 : /bin/zsh
- 터미널 : xterm-256color
- Docker 버전 : Docker version 28.5.2, build ecc6942
- Git 버전 : git version 2.53.0
```
Last login: Tue Mar 31 20:26:34 on ttys000
na908158800@c3r1s4 ~ % system_profiler SPSoftwareDataType 
Software:

    System Software Overview:

      System Version: macOS 15.7.4 (24G517)
      Kernel Version: Darwin 24.6.0
      Boot Volume: Macintosh HD
      Boot Mode: Normal
      Computer Name: c3r1s4.codyssey.kr
      User Name: 김권우 (na908158800)
      Secure Virtual Memory: Enabled
      System Integrity Protection: Disabled
      Time since boot: 1 day, 2 hours, 10 minutes

na908158800@c3r1s4 ~ % echo $SHELL
/bin/zsh
na908158800@c3r1s4 ~ % echo $TERM
xterm-256color
na908158800@c3r1s4 ~ % docker --version
Docker version 28.5.2, build ecc6942
na908158800@c3r1s4 ~ % git --version
git version 2.53.0
```



# 수행항목 체크리스트
[x] 터미널 조작로그
```
Last login: Wed Apr  1 11:09:12 on ttys000
na908158800@c3r1s4 ~ % pwd
/Users/na908158800
na908158800@c3r1s4 ~ % ls
571712656-43d9438a-2468-4a0f-8841-3516ab2dc998.png
Desktop
Documents
Downloads
Library
Movies
Music
OrbStack
Pictures
Public
file_copy.txt
permission_test
na908158800@c3r1s4 ~ % ls -la
total 968
drwxr-x---+ 23 na908158800  na908158800     736 Apr  1 11:11 .
drwxr-xr-x   7 root         admin           224 Mar 31 08:59 ..
-r--------   1 na908158800  na908158800       7 Mar 31 08:59 .CFUserTextEncoding
-rw-r--r--@  1 na908158800  na908158800    8196 Mar 31 09:50 .DS_Store
drwx------+ 82 na908158800  na908158800    2624 Apr  1 10:29 .Trash
drwxr-xr-x   5 na908158800  na908158800     160 Mar 31 09:03 .docker
drwxr-xr-x  10 na908158800  na908158800     320 Mar 31 10:41 .orbstack
drwxr-xr-x   3 na908158800  na908158800      96 Mar 31 09:03 .ssh
drwxr-xr-x   3 na908158800  na908158800      96 Mar 31 09:03 .vscode
-rw-------   1 na908158800  na908158800    1663 Apr  1 11:11 .zsh_history
drwx------  36 na908158800  na908158800    1152 Apr  1 11:11 .zsh_sessions
-rw-r--r--@  1 na908158800  na908158800  467942 Mar 31 17:50 571712656-43d9438a-2468-4a0f-8841-3516ab2dc998.png
drwx------+  9 na908158800  na908158800     288 Apr  1 10:38 Desktop
drwx------+  3 na908158800  na908158800      96 Mar 31 08:59 Documents
drwx------+  6 na908158800  na908158800     192 Apr  1 10:21 Downloads
drwx------@ 80 na908158800  na908158800    2560 Mar 31 14:00 Library
drwx------   4 na908158800  na908158800     128 Apr  1 09:07 Movies
drwx------+  3 na908158800  na908158800      96 Mar 31 08:59 Music
drwx------   4 na908158800  na908158800     160 Mar 31 10:41 OrbStack
drwx------+  4 na908158800  na908158800     128 Mar 31 09:00 Pictures
drwxr-xr-x+  4 na908158800  na908158800     128 Mar 31 08:59 Public
-rw-r--r--   1 na908158800  na908158800       6 Mar 31 14:55 file_copy.txt
drwxr-xr-x   4 na908158800  na908158800     128 Mar 31 17:08 permission_test
na908158800@c3r1s4 ~ % mkdir test_dir
na908158800@c3r1s4 ~ % ls
571712656-43d9438a-2468-4a0f-8841-3516ab2dc998.png
Desktop
Documents
Downloads
Library
Movies
Music
OrbStack
Pictures
Public
file_copy.txt
permission_test
test_dir
na908158800@c3r1s4 ~ % touch file_txt
na908158800@c3r1s4 ~ % ls -la
total 968
drwxr-x---+ 25 na908158800  na908158800     800 Apr  1 11:12 .
drwxr-xr-x   7 root         admin           224 Mar 31 08:59 ..
-r--------   1 na908158800  na908158800       7 Mar 31 08:59 .CFUserTextEncoding
-rw-r--r--@  1 na908158800  na908158800    8196 Mar 31 09:50 .DS_Store
drwx------+ 82 na908158800  na908158800    2624 Apr  1 10:29 .Trash
drwxr-xr-x   5 na908158800  na908158800     160 Mar 31 09:03 .docker
drwxr-xr-x  10 na908158800  na908158800     320 Mar 31 10:41 .orbstack
drwxr-xr-x   3 na908158800  na908158800      96 Mar 31 09:03 .ssh
drwxr-xr-x   3 na908158800  na908158800      96 Mar 31 09:03 .vscode
-rw-------   1 na908158800  na908158800    1663 Apr  1 11:11 .zsh_history
drwx------  36 na908158800  na908158800    1152 Apr  1 11:11 .zsh_sessions
-rw-r--r--@  1 na908158800  na908158800  467942 Mar 31 17:50 571712656-43d9438a-2468-4a0f-8841-3516ab2dc998.png
drwx------+  9 na908158800  na908158800     288 Apr  1 10:38 Desktop
drwx------+  3 na908158800  na908158800      96 Mar 31 08:59 Documents
drwx------+  6 na908158800  na908158800     192 Apr  1 10:21 Downloads
drwx------@ 80 na908158800  na908158800    2560 Mar 31 14:00 Library
drwx------   4 na908158800  na908158800     128 Apr  1 09:07 Movies
drwx------+  3 na908158800  na908158800      96 Mar 31 08:59 Music
drwx------   4 na908158800  na908158800     160 Mar 31 10:41 OrbStack
drwx------+  4 na908158800  na908158800     128 Mar 31 09:00 Pictures
drwxr-xr-x+  4 na908158800  na908158800     128 Mar 31 08:59 Public
-rw-r--r--   1 na908158800  na908158800       6 Mar 31 14:55 file_copy.txt
-rw-r--r--   1 na908158800  na908158800       0 Apr  1 11:12 file_txt
drwxr-xr-x   4 na908158800  na908158800     128 Mar 31 17:08 permission_test
drwxr-xr-x   2 na908158800  na908158800      64 Apr  1 11:12 test_dir
na908158800@c3r1s4 ~ % cat file.txt
cat: file.txt: No such file or directory
na908158800@c3r1s4 ~ % echo "Hello"> file.txt
na908158800@c3r1s4 ~ % cat file.txt
Hello
na908158800@c3r1s4 ~ % cp file.txt file_copy.txt
na908158800@c3r1s4 ~ % ls -la
total 976
drwxr-x---+ 26 na908158800  na908158800     832 Apr  1 11:15 .
drwxr-xr-x   7 root         admin           224 Mar 31 08:59 ..
-r--------   1 na908158800  na908158800       7 Mar 31 08:59 .CFUserTextEncoding
-rw-r--r--@  1 na908158800  na908158800    8196 Mar 31 09:50 .DS_Store
drwx------+ 82 na908158800  na908158800    2624 Apr  1 10:29 .Trash
drwxr-xr-x   5 na908158800  na908158800     160 Mar 31 09:03 .docker
drwxr-xr-x  10 na908158800  na908158800     320 Mar 31 10:41 .orbstack
drwxr-xr-x   3 na908158800  na908158800      96 Mar 31 09:03 .ssh
drwxr-xr-x   3 na908158800  na908158800      96 Mar 31 09:03 .vscode
-rw-------   1 na908158800  na908158800    1663 Apr  1 11:11 .zsh_history
drwx------  36 na908158800  na908158800    1152 Apr  1 11:11 .zsh_sessions
-rw-r--r--@  1 na908158800  na908158800  467942 Mar 31 17:50 571712656-43d9438a-2468-4a0f-8841-3516ab2dc998.png
drwx------+  9 na908158800  na908158800     288 Apr  1 10:38 Desktop
drwx------+  3 na908158800  na908158800      96 Mar 31 08:59 Documents
drwx------+  6 na908158800  na908158800     192 Apr  1 10:21 Downloads
drwx------@ 80 na908158800  na908158800    2560 Mar 31 14:00 Library
drwx------   4 na908158800  na908158800     128 Apr  1 09:07 Movies
drwx------+  3 na908158800  na908158800      96 Mar 31 08:59 Music
drwx------   4 na908158800  na908158800     160 Mar 31 10:41 OrbStack
drwx------+  4 na908158800  na908158800     128 Mar 31 09:00 Pictures
drwxr-xr-x+  4 na908158800  na908158800     128 Mar 31 08:59 Public
-rw-r--r--   1 na908158800  na908158800       6 Apr  1 11:15 file.txt
-rw-r--r--   1 na908158800  na908158800       6 Apr  1 11:17 file_copy.txt
-rw-r--r--   1 na908158800  na908158800       0 Apr  1 11:12 file_txt
drwxr-xr-x   4 na908158800  na908158800     128 Mar 31 17:08 permission_test
drwxr-xr-x   2 na908158800  na908158800      64 Apr  1 11:12 test_dir
na908158800@c3r1s4 ~ % mv renamed.txt ..
mv: rename renamed.txt to ../renamed.txt: No such file or directory
na908158800@c3r1s4 ~ % mv file.txt renamed.txt
na908158800@c3r1s4 ~ % mv renamed.txt ..
mv: rename renamed.txt to ../renamed.txt: Permission denied
na908158800@c3r1s4 ~ % mv renamed.txt test_dir/
na908158800@c3r1s4 ~ % ls -la
total 968
drwxr-x---+ 25 na908158800  na908158800     800 Apr  1 11:20 .
drwxr-xr-x   7 root         admin           224 Mar 31 08:59 ..
-r--------   1 na908158800  na908158800       7 Mar 31 08:59 .CFUserTextEncoding
-rw-r--r--@  1 na908158800  na908158800    8196 Mar 31 09:50 .DS_Store
drwx------+ 82 na908158800  na908158800    2624 Apr  1 10:29 .Trash
drwxr-xr-x   5 na908158800  na908158800     160 Mar 31 09:03 .docker
drwxr-xr-x  10 na908158800  na908158800     320 Mar 31 10:41 .orbstack
drwxr-xr-x   3 na908158800  na908158800      96 Mar 31 09:03 .ssh
drwxr-xr-x   3 na908158800  na908158800      96 Mar 31 09:03 .vscode
-rw-------   1 na908158800  na908158800    1663 Apr  1 11:11 .zsh_history
drwx------  36 na908158800  na908158800    1152 Apr  1 11:11 .zsh_sessions
-rw-r--r--@  1 na908158800  na908158800  467942 Mar 31 17:50 571712656-43d9438a-2468-4a0f-8841-3516ab2dc998.png
drwx------+  9 na908158800  na908158800     288 Apr  1 10:38 Desktop
drwx------+  3 na908158800  na908158800      96 Mar 31 08:59 Documents
drwx------+  6 na908158800  na908158800     192 Apr  1 10:21 Downloads
drwx------@ 80 na908158800  na908158800    2560 Mar 31 14:00 Library
drwx------   4 na908158800  na908158800     128 Apr  1 09:07 Movies
drwx------+  3 na908158800  na908158800      96 Mar 31 08:59 Music
drwx------   4 na908158800  na908158800     160 Mar 31 10:41 OrbStack
drwx------+  4 na908158800  na908158800     128 Mar 31 09:00 Pictures
drwxr-xr-x+  4 na908158800  na908158800     128 Mar 31 08:59 Public
-rw-r--r--   1 na908158800  na908158800       6 Apr  1 11:17 file_copy.txt
-rw-r--r--   1 na908158800  na908158800       0 Apr  1 11:12 file_txt
drwxr-xr-x   4 na908158800  na908158800     128 Mar 31 17:08 permission_test
drwxr-xr-x   3 na908158800  na908158800      96 Apr  1 11:20 test_dir
na908158800@c3r1s4 ~ % cd test_dir 
na908158800@c3r1s4 test_dir % ls -la 
total 8
drwxr-xr-x   3 na908158800  na908158800   96 Apr  1 11:20 .
drwxr-x---+ 25 na908158800  na908158800  800 Apr  1 11:20 ..
-rw-r--r--   1 na908158800  na908158800    6 Apr  1 11:15 renamed.txt
na908158800@c3r1s4 test_dir % rm renamed.txt
na908158800@c3r1s4 test_dir % ls -la
total 0
drwxr-xr-x   2 na908158800  na908158800   64 Apr  1 11:22 .
drwxr-x---+ 25 na908158800  na908158800  800 Apr  1 11:20 ..
na908158800@c3r1s4 test_dir % cd ..
na908158800@c3r1s4 ~ % rmdir test_dir
na908158800@c3r1s4 ~ % ls
571712656-43d9438a-2468-4a0f-8841-3516ab2dc998.png
Desktop
Documents
Downloads
Library
Movies
Music
OrbStack
Pictures
Public
file_copy.txt
file_txt
permission_test
```

[x] 권한 확인 및 변경
```
Last login: Wed Apr  1 11:11:25 on ttys000
na908158800@c3r1s4 ~ % cd permission_test
na908158800@c3r1s4 permission_test % ls -la
total 8
drwxr-xr-x   4 na908158800  na908158800  128 Mar 31 17:08 .
drwxr-x---+ 24 na908158800  na908158800  768 Apr  1 11:23 ..
drwx--xr-x   3 na908158800  na908158800   96 Mar 31 17:09 test_directory
-rw-------   1 na908158800  na908158800   20 Mar 31 17:08 test_file.txt
na908158800@c3r1s4 permission_test % ls -l test_file.txt
-rw-------  1 na908158800  na908158800  20 Mar 31 17:08 test_file.txt
na908158800@c3r1s4 permission_test % ls -ld test_directory
drwx--xr-x  3 na908158800  na908158800  96 Mar 31 17:09 test_directory
na908158800@c3r1s4 permission_test % chomod g-r test_file.txt
zsh: command not found: chomod
na908158800@c3r1s4 permission_test % chmod g-r test_file.txt
na908158800@c3r1s4 permission_test % ls -l test_file.txt 
-rw-------  1 na908158800  na908158800  20 Mar 31 17:08 test_file.txt
na908158800@c3r1s4 permission_test % chmod g+r test_file.txt
na908158800@c3r1s4 permission_test % ls -l test_file.txt
-rw-r-----  1 na908158800  na908158800  20 Mar 31 17:08 test_file.txt
na908158800@c3r1s4 permission_test % chmod 722 test_directory
na908158800@c3r1s4 permission_test % ls -ld test_directory
drwx-w--w-  3 na908158800  na908158800  96 Mar 31 17:09 test_directory
```
[x] Docker 운영/검증
<img width="1394" height="658" alt="image" src="https://github.com/user-attachments/assets/6d737afa-c51f-4a9a-a5d3-719aaa741528" />


[] Dockerfile
[] 포트
[] 볼륨
[] Git
[] GitHub

# 트러블 슈팅 2건 이상 (문제 → 원인 가설 → 확인 → 해결/대안)
- 터미널 조작시, 파일이 상위 폴더로 이동되지 않는 문제 
  ☞ 가설 : 현재 위치가 최상위라서 더이상 이동할수 없음
  ☞ 확인 : 최상위 폴더는 아니었고, 상위폴더가 유저라서 권한이 없음.
  ☞ 해결 : 하위폴더로는 해당 명령어로 정상 이동됨 확인
- docker Container 실행시, 로그 확인되지 않는 문제
  ☞ 가설 : 로그 출력할 이벤트가 발생하지 않음
  ☞ 확인 : Sleep 명령어 사용으로, 쉬는 중이므로 로그출력되지 않는 것이 정상
  ☞ 해결 : 정상 상황이므로 해결 불필요

# Dockerfile 기반 웹서버 컨테이너
- 웹 서버 소스코드(예: app/ 또는 src/)
- Dockerfile
- 빌드/실행 명령 및 결과 로그(터미널 스크린샷 가능)
- 포트 매핑 접속 성공 증거(스크린샷 또는 로그)
# 포트 매핑 접속 증거
- p <host_port>:<container_port>로 실행 후, 브라우저 접속 화면(주소창 포함)을 기술 문서에 첨부한다.
# 바인드 마운트 반영 + 볼륨 영속성 증거
- 바인드 마운트: 실행 명령 + 호스트 변경 전/후 비교
- Docker 볼륨: 생성/연결/검증 명령 + 컨테이너 삭제 전/후 비교
# Git 설정 및 GitHub/VSCode 연동 증거
- Git 사용자 정보·기본 브랜치 설정 후, VSCode에서 GitHub 로그인 및 저장소 연동 완료
- 민감한 개인 정보(ID/PW, 토큰 등)가 포함되지 않도록 주의한다.



 # 요구사항
1. 
    - 수행 항목 체크리스트(터미널/권한/Docker/Dockerfile/포트/마운트/볼륨/Git/GitHub)
    - 검증 방법(어떤 명령으로 무엇을 확인했는지) + 결과 위치/증거 링크
  - 기술 문서 내 명령/출력은 코드블록으로 정리한다.
