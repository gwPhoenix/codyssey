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
<img width="1394" height="966" alt="image" src="https://github.com/user-attachments/assets/f81a1771-2b19-448a-8a62-93c042a6d177" />

# 수행항목 체크리스트
[] 터미널
[] 권한
[] Docker
[] Dockerfile
[] 포트
[] 볼륨
[] Git
[] GitHub

# 검증방법 (어떤 명령으로 무엇을 확인했는지) + 결과위치 링크
# 트러블 슈팅 2건 이상 (문제 → 원인 가설 → 확인 → 해결/대안)

# 터미널 조작로그
# Docker 운영/검증 로그
- docker --version, docker info 등 설치·점검 결과
- docker images, docker ps -a, docker logs, docker stats 등 운영 명령 실행 흔적
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
  - GitHub Repository 링크로 제출한다.
  - 기술 문서(README.md 등)는 아래 내용을 반드시 포함한다.
    - 모든 수행 결과는 “기술 문서(README.md 등)”에서 확인 가능해야 한다.
    - 프로젝트 개요(미션 목표 요약)
    - 실행 환경(OS/쉘/터미널, Docker 버전, Git 버전)
    - 수행 항목 체크리스트(터미널/권한/Docker/Dockerfile/포트/마운트/볼륨/Git/GitHub)
    - 검증 방법(어떤 명령으로 무엇을 확인했는지) + 결과 위치/증거 링크
  - 기술 문서 내 명령/출력은 코드블록으로 정리한다.
