# inception

> 42 Gyeongsan — Circle 5

Docker와 Docker Compose를 이용해 **WordPress + MariaDB + Nginx** 스택을 컨테이너로 구성하는 인프라 프로젝트입니다.  
외부 이미지 사용 없이 `Dockerfile`을 직접 작성하여 각 서비스를 빌드합니다.

---

## 아키텍처

```
         HTTPS (포트 443)
              │
              ▼
        ┌──────────┐
        │  Nginx   │  ← TLS 종단, 리버스 프록시
        └────┬─────┘
             │ (내부 네트워크)
             ▼
        ┌──────────┐
        │WordPress │  ← PHP-FPM, CMS
        └────┬─────┘
             │
             ▼
        ┌──────────┐
        │ MariaDB  │  ← 데이터베이스
        └──────────┘
```

---

## 구성 요소

| 서비스 | 기반 이미지 | 역할 |
|--------|------------|------|
| **Nginx** | Debian slim | HTTPS 종단(TLS 1.2/1.3), 리버스 프록시 |
| **WordPress** | Debian slim | PHP-FPM, WordPress CMS |
| **MariaDB** | Debian slim | 관계형 데이터베이스 |

> 모든 이미지는 `alpine` 또는 `debian` 베이스에서 직접 빌드 (Docker Hub 완성 이미지 사용 금지)

---

## 주요 설정 내용

### Docker Compose
- 전용 네트워크로 서비스 간 격리
- 볼륨으로 DB 데이터 및 WordPress 파일 영속화
- `depends_on`으로 서비스 시작 순서 보장
- `.env` 파일로 민감 정보(DB 비밀번호 등) 분리

### Nginx
- 자체 서명 SSL/TLS 인증서 (OpenSSL)
- PHP 요청을 WordPress(PHP-FPM socker_fd)로 프록시
- TLS 1.2 이상만 허용

### MariaDB
- 환경변수로 DB명, 사용자, 비밀번호 자동 초기화
- 루트 원격 접속 비활성화

---

## 실행 방법

```bash
make        # Docker Compose 빌드 및 실행
make down   # 서비스 중지
make clean  # 컨테이너 + 볼륨 제거
```

접속: `https://login.42.fr`

---

## 배운 점

- `Dockerfile` 직접 작성: `RUN`, `COPY`, `ENTRYPOINT`, `CMD`, `EXPOSE`
- Docker 볼륨과 바인드 마운트의 차이와 데이터 영속화
- Docker 네트워크와 컨테이너 간 DNS 기반 통신
- Nginx 리버스 프록시 설정 및 TLS 인증서 관리
- 멀티 컨테이너 오케스트레이션과 서비스 의존성 관리
- 환경변수로 설정을 분리하는 12-Factor App 원칙
