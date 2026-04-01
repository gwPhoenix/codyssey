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
<img width="1394" height="1134" alt="image" src="https://github.com/user-attachments/assets/a77f6866-c8b8-4d12-bcb9-a7f82811dbaf" />
<img width="1394" height="1134" alt="image" src="https://github.com/user-attachments/assets/dc4aa6d0-9d55-4748-8c90-31ba5520ea87" />
<img width="1394" height="1246" alt="image" src="https://github.com/user-attachments/assets/74c8702f-c4bd-4a89-9a14-b548caf9e18b" />
<img width="1394" height="770" alt="image" src="https://github.com/user-attachments/assets/b45ed1b8-5dc8-4d7e-9653-c0ec9b20ba6f" />

[x] 권한 확인 및 변경
<img width="1394" height="966" alt="image" src="https://github.com/user-attachments/assets/0c214b5f-b82c-4048-a6e1-e4c1a11358c2" />
[x] Docker 운영/검증
<img width="1394" height="2870" alt="image" src="https://github.com/user-attachments/assets/e4831d07-5c1a-450c-aaef-bfd3421a7dcc" />
<img width="1394" height="686" alt="image" src="https://github.com/user-attachments/assets/ce0147c2-8567-4aa5-8648-d0ea16434b2b" />
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
