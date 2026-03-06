# born2beroot

> 42 Gyeongsan — Circle 1

VirtualBox를 사용해 Debian Linux 가상 머신을 처음부터 구축하고 보안 정책을 직접 설정한 시스템 관리 프로젝트입니다.

---

## 구현 내용

### 가상 머신 환경
- **OS:** Debian GNU/Linux (최신 Stable)
- **하이퍼바이저:** VirtualBox
- **파티셔닝:** LVM 암호화 파티션 (`/`, `/home`, `/var`, `/srv`, `/tmp`, `/var/log` 등 분리)

### 보안 설정

| 항목 | 설정 내용 |
|------|----------|
| **SSH** | 포트 4242로 변경, root 직접 로그인 금지 |
| **UFW 방화벽** | 포트 4242만 허용 |
| **sudo 정책** | 비밀번호 3회 시도 제한, 로그 기록 (`/var/log/sudo`), TTY 강제, 경로 제한 |
| **비밀번호 정책** | 30일 만료, 최소 10자, 대문자/숫자/특수문자 포함 |
| **hostname** | `djang42` 형식 |

### 모니터링 스크립트
`monitoring.sh` — cron으로 10분마다 자동 실행:
- OS / 커널 버전
- CPU 물리/가상 수
- RAM / 디스크 사용량
- CPU 사용률
- 마지막 재부팅 시간
- LVM 활성화 여부
- TCP 연결 수
- 로그인 사용자 수
- IP / MAC 주소
- sudo 실행 횟수

---

## 배운 점

- Linux 파티셔닝 구조와 LVM(Logical Volume Manager) 개념
- 서버 보안의 기본 — 최소 권한 원칙, sudo 감사 로그
- UFW, SSH 데몬 설정 및 방화벽 규칙
- cron을 이용한 스케줄링 자동화
- systemd 서비스와 AppArmor 기초
