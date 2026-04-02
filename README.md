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
na908158800@c3r1s4 ~ % system_profiler SPSoftwareDataType   #운영체제 확인(맥용)
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

na908158800@c3r1s4 ~ % echo $SHELL   #쉘 확인
/bin/zsh
na908158800@c3r1s4 ~ % echo $TERM   #터미널 확인
xterm-256color
na908158800@c3r1s4 ~ % docker --version   #도커 버전 확인
Docker version 28.5.2, build ecc6942
na908158800@c3r1s4 ~ % git --version   # 깃 버전 확인
git version 2.53.0
```



# 수행항목 체크리스트
[x] 터미널 조작로그
```
Last login: Wed Apr  1 11:09:12 on ttys000
na908158800@c3r1s4 ~ % pwd   #현재 경로 확인
/Users/na908158800
na908158800@c3r1s4 ~ % ls   #폴더와 파일 목록 확인
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
na908158800@c3r1s4 ~ % ls -la   #폴더와 파일 목록 확인(숨김파일 포함, 상세내용)
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
```
```
na908158800@c3r1s4 ~ % mkdir test_dir   #디렉토리 생성
na908158800@c3r1s4 ~ % ls   #폴더와 파일 목록 확인
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
test_dir    #추가된 디렉토리
na908158800@c3r1s4 ~ % touch empty_file.txt   #파일 생성(내용 없음)
na908158800@c3r1s4 ~ % ls -la   #폴더와 파일 목록 확인(숨김파일 포함, 상세내용)
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
-rw-r--r--   1 na908158800  na908158800       0 Apr  1 11:12 empty_file.txt   #추가된 파일
drwxr-xr-x   4 na908158800  na908158800     128 Mar 31 17:08 permission_test
drwxr-xr-x   2 na908158800  na908158800      64 Apr  1 11:12 test_dir
```
```
na908158800@c3r1s4 ~ % cat empty_file.txt   #방금 생성한 빈파일 내용 확인 ▶︎ 출력결과 없음
na908158800@c3r1s4 ~ % echo "Hello"> empty_file.txt   #빈 파일에 내용 추가
na908158800@c3r1s4 ~ % cat empty_file.txt   #내용 추가한 파일내용 확인
Hello   #파일 내용 "Hello" 출력
na908158800@c3r1s4 ~ % cp empty_file.txt file_copy.txt   #엠티파일 기준  "file_copy.txt"로 복사
na908158800@c3r1s4 ~ % ls -la   #폴더와 파일 목록 확인(숨김파일 포함, 상세내용)
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
-rw-r--r--   1 na908158800  na908158800       6 Apr  1 11:17 file_copy.txt   #추가된 복사파일
-rw-r--r--   1 na908158800  na908158800       0 Apr  1 11:12 empty_file.txt
drwxr-xr-x   4 na908158800  na908158800     128 Mar 31 17:08 permission_test
drwxr-xr-x   2 na908158800  na908158800      64 Apr  1 11:12 test_dir
```
```
na908158800@c3r1s4 ~ % mv empty_file.txt renamed.txt   #엠타파일 이름을 " rename.txt "로 변경
na908158800@c3r1s4 ~ % mv renamed.txt ..   #현재 경로 기준 상위폴더로 이동
mv: rename renamed.txt to ../renamed.txt: Permission denied   #상위폴더로 이동권한이 없음
na908158800@c3r1s4 ~ % mv renamed.txt test_dir/   #test_dir 디렉토리에 파일이동
na908158800@c3r1s4 ~ % ls -la   #폴더와 파일 목록 확인(숨김파일 포함, 상세내용) ▶︎ 파일이 이동되어 목록에 없음
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
drwxr-xr-x   4 na908158800  na908158800     128 Mar 31 17:08 permission_test
drwxr-xr-x   3 na908158800  na908158800      96 Apr  1 11:20 test_dir
na908158800@c3r1s4 ~ % cd test_dir   #해당 디렉토리로 이동
na908158800@c3r1s4 test_dir % ls -la   #폴더와 파일 목록 확인(숨김파일 포함, 상세내용)
total 8
drwxr-xr-x   3 na908158800  na908158800   96 Apr  1 11:20 .
drwxr-x---+ 25 na908158800  na908158800  800 Apr  1 11:20 ..
-rw-r--r--   1 na908158800  na908158800    6 Apr  1 11:15 renamed.txt   #이동된 파일
na908158800@c3r1s4 test_dir % rm renamed.txt   #해당 파일 삭제
na908158800@c3r1s4 test_dir % ls -la   #폴더와 파일 목록 확인(숨김파일 포함, 상세내용) ▶︎ 파일 삭제되어 목록에 없음
total 0
drwxr-xr-x   2 na908158800  na908158800   64 Apr  1 11:22 .
drwxr-x---+ 25 na908158800  na908158800  800 Apr  1 11:20 ..
```
```
na908158800@c3r1s4 test_dir % cd ..   #상위 폴더 디렉토리로 이동
na908158800@c3r1s4 ~ % rmdir test_dir   # 해당 디렉토리 삭제
na908158800@c3r1s4 ~ % ls   #폴더와 파일 목록 확인 ▶︎ 디렉토리 삭제되어 목록에 없음
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
```

<br>

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

<br>

[x] Docker 운영/검증
```
Last login: Wed Apr  1 11:28:50 on ttys000
na908158800@c3r1s4 ~ % docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
na908158800@c3r1s4 ~ % docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
817807f3c64e: Already exists 
Digest: sha256:186072bba1b2f436cbb91ef2567abca677337cfc786c86e107d25b7072feef0c
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
na908158800@c3r1s4 ~ % docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    f794f40ddfff   5 weeks ago   78.1MB
na908158800@c3r1s4 ~ % docker run -d --name myapp ubuntu sleep 1000
docker: Error response from daemon: Conflict. The container name "/myapp" is already in use by container "883060181ac08dee9ce924f40eed0bef13e4869c47a4c4d1bca2c9d2937c0725". You have to remove (or rename) that container to be able to reuse that name.

Run 'docker run --help' for more information
na908158800@c3r1s4 ~ % docker rm myapp
myapp
na908158800@c3r1s4 ~ % docker run -d --name myapp ubuntu sleep 1000
767cb24e58a3729551182c0efcaee43228f40f0fb31c51c4b8efe65342144b25
na908158800@c3r1s4 ~ % docker ps
CONTAINER ID   IMAGE     COMMAND        CREATED         STATUS         PORTS     NAMES
767cb24e58a3   ubuntu    "sleep 1000"   7 seconds ago   Up 7 seconds             myapp
na908158800@c3r1s4 ~ % docker logs myapp
na908158800@c3r1s4 ~ % docker stop myapp
myapp
na908158800@c3r1s4 ~ % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
```
Last login: Wed Apr  1 11:43:03 on ttys000
na908158800@c3r1s4 ~ % docker run -d ubuntu sleep 1000
4cb893e2d5c86fab460cd435763a6cef9bacadb489e87fded863acc3680ea450
na908158800@c3r1s4 ~ % docekr stats


CONTAINER ID   NAME                  CPU %     MEM USAGE / LIMIT     MEM %     NET I/O         BLOCK I/O     PIDS 
57826daaccee   romantic_montalcini   0.00%     3.145MiB / 15.67GiB   0.02%     1.13kB / 126B   2.52MB / 0B   1 
```

<br>

[x] docker - Hello-World
- hello-world 실행
```
Last login: Wed Apr  1 12:00:13 on ttys000

na908158800@c3r1s4 ~ % docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
```
Last login: Wed Apr  1 12:19:20 on ttys000
na908158800@c3r1s4 ~ % docker run hello-world> hello-world-result.log 2>&1
na908158800@c3r1s4 ~ % cat hello-world-result.log

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
- Ubuntu 컨테이너 실행 및 내부 진입
```
na908158800@c3r1s4 ~ % docker run -it ubuntu bash
root@50eb7c1cbe60:/# ls
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
root@50eb7c1cbe60:/# ls -la
total 16
drwxr-xr-x   1 root root   6 Apr  1 03:22 .
drwxr-xr-x   1 root root   6 Apr  1 03:22 ..
-rwxr-xr-x   1 root root   0 Apr  1 03:22 .dockerenv
lrwxrwxrwx   1 root root   7 Apr 22  2024 bin -> usr/bin
drwxr-xr-x   1 root root   0 Apr 22  2024 boot
drwxr-xr-x   5 root root 340 Apr  1 03:22 dev
drwxr-xr-x   1 root root  56 Apr  1 03:22 etc
drwxr-xr-x   1 root root  12 Feb 17 02:09 home
lrwxrwxrwx   1 root root   7 Apr 22  2024 lib -> usr/lib
lrwxrwxrwx   1 root root   9 Apr 22  2024 lib64 -> usr/lib64
drwxr-xr-x   1 root root   0 Feb 17 02:02 media
drwxr-xr-x   1 root root   0 Feb 17 02:02 mnt
drwxr-xr-x   1 root root   0 Feb 17 02:02 opt
dr-xr-xr-x 229 root root   0 Apr  1 03:22 proc
drwx------   1 root root  30 Feb 17 02:09 root
drwxr-xr-x   1 root root  22 Feb 17 02:09 run
lrwxrwxrwx   1 root root   8 Apr 22  2024 sbin -> usr/sbin
drwxr-xr-x   1 root root   0 Feb 17 02:02 srv
dr-xr-xr-x  11 root root   0 Apr  1 03:22 sys
drwxrwxrwt   1 root root   0 Feb 17 02:09 tmp
drwxr-xr-x   1 root root  10 Feb 17 02:02 usr
drwxr-xr-x   1 root root  90 Feb 17 02:09 var
root@50eb7c1cbe60:/# pwd
/
root@50eb7c1cbe60:/# echo $HOME
/root
root@50eb7c1cbe60:/# uname -a
Linux 50eb7c1cbe60 6.17.8-orbstack-00308-g8f9c941121b1 #1 SMP PREEMPT Thu Nov 20 09:34:02 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
root@50eb7c1cbe60:/# hostname
50eb7c1cbe60
root@50eb7c1cbe60:/# echo "Hello from Docker Container"> test.txt
root@50eb7c1cbe60:/# cat test.txt
Hello from Docker Container
root@50eb7c1cbe60:/# exit
exit
```
- attach vs exec 차이 관찰
  - attach : exit할 경우, 컨테이너 종료
  - exec : exit해도 컨테이너 유지, 실행중인 컨테이너에 새로운 프로세스 가능
```
Last login: Wed Apr  1 12:50:17 on ttys000
na908158800@c3r1s4 ~ % docker run -it -d --name my-ubuntu ubuntu bash
adb9b14afd51011a460b0102e5a7f0d037851eebae4cf31f8fb34634d5c68422
na908158800@c3r1s4 ~ % docker attach my-ubuntu
root@adb9b14afd51:/# ls
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
root@adb9b14afd51:/# echo "attach test"
attach test
root@adb9b14afd51:/# exit
exit
na908158800@c3r1s4 ~ % docker exec -it my-ubuntu bash
Error response from daemon: container adb9b14afd51011a460b0102e5a7f0d037851eebae4cf31f8fb34634d5c68422 is not running
na908158800@c3r1s4 ~ % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
na908158800@c3r1s4 ~ % docker ps -a
CONTAINER ID   IMAGE         COMMAND        CREATED             STATUS                           PORTS     NAMES
adb9b14afd51   ubuntu        "bash"         4 minutes ago       Exited (0) 3 minutes ago                   my-ubuntu
d39d00141b17   ubuntu        "bash"         14 minutes ago      Exited (0) 14 minutes ago                  test_ubuntu
50eb7c1cbe60   ubuntu        "bash"         37 minutes ago      Exited (0) 34 minutes ago                  quirky_kepler
9dbb17caec5a   hello-world   "/hello"       38 minutes ago      Exited (0) 38 minutes ago                  crazy_hawking
692568505c42   hello-world   "/hello"       40 minutes ago      Exited (0) 40 minutes ago                  suspicious_ishizaka
d7d84f80f253   ubuntu        "bash"         41 minutes ago      Exited (129) 40 minutes ago                wonderful_greider
268a450df7d4   hello-world   "/hello"       46 minutes ago      Exited (0) 46 minutes ago                  eager_knuth
4eb0bc6f3ff1   hello-world   "/hello"       47 minutes ago      Exited (0) 47 minutes ago                  dazzling_sinoussi
4cb893e2d5c8   ubuntu        "sleep 1000"   About an hour ago   Exited (0) 58 minutes ago                  strange_wing
57826daaccee   ubuntu        "sleep 1000"   About an hour ago   Exited (0) 59 minutes ago                  romantic_montalcini
767cb24e58a3   ubuntu        "sleep 1000"   About an hour ago   Exited (137) About an hour ago             myapp
na908158800@c3r1s4 ~ % docker start my-ubuntu
my-ubuntu
na908158800@c3r1s4 ~ % docker exec -it my-ubuntu bash
root@adb9b14afd51:/# ls
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
root@adb9b14afd51:/# echo "exec test"
exec test
root@adb9b14afd51:/# pwd
/
root@adb9b14afd51:/# exit
exit
na908158800@c3r1s4 ~ % 
```

<br>

[x] 기존 Dockerfile 기반 커스텀 이미지 제작

```

```

<br>

[x] 포트 매핑 & 브라우저 접속
- Host Port: 8080
- Container Port: 80
- 접속 URL: http://localhost:8080
```
Last login: Wed Apr  1 15:26:36 on ttys000
na908158800@c3r1s4 ~ % docker run -d -p 8080:80 my-web-app:1.0
eb25fe9ffed84e066d22812565b1cbfff04b99a1f4643d76c93a4d7792ce93b6
na908158800@c3r1s4 ~ % docker ps
CONTAINER ID   IMAGE            COMMAND                  CREATED          STATUS          PORTS                                     NAMES
eb25fe9ffed8   my-web-app:1.0   "/docker-entrypoint.…"   13 seconds ago   Up 12 seconds   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   quirky_gauss
adb9b14afd51   ubuntu           "bash"                   3 hours ago      Up 2 hours   
```
<img width="2020" height="284" alt="image" src="https://github.com/user-attachments/assets/8c3964d1-d700-4880-9594-35384ae507d6" />


<br>

[] 바인드 마운트 반영 + 볼륨 영속성

<br>

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


# 바인드 마운트 반영 + 볼륨 영속성 증거
- 바인드 마운트: 실행 명령 + 호스트 변경 전/후 비교
- Docker 볼륨: 생성/연결/검증 명령 + 컨테이너 삭제 전/후 비교
# Git 설정 및 GitHub/VSCode 연동 증거
- Git 사용자 정보·기본 브랜치 설정 후, VSCode에서 GitHub 로그인 및 저장소 연동 완료
- 민감한 개인 정보(ID/PW, 토큰 등)가 포함되지 않도록 주의한다.
