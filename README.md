# 42 Gyeongsan — djang의 커먼코어 포트폴리오

> 42 Gyeongsan에서 수행한 **Common Core** 과제들을 정리한 레포지토리입니다.  
> C 언어 저수준 프로그래밍부터 풀스택 웹 개발까지, 약 1년간의 학습 여정을 담았습니다.

---

## 🛠 기술 스택

**시스템 프로그래밍**  
![C](https://img.shields.io/badge/C-00599C?style=flat&logo=c&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat&logo=cplusplus&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)

**웹 / 풀스택**  
![React](https://img.shields.io/badge/React-20232A?style=flat&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat&logo=typescript&logoColor=white)
![Node.js](https://img.shields.io/badge/Fastify-000000?style=flat&logo=fastify&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=flat&logo=mariadb&logoColor=white)

**인프라 / DevOps**  
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![WebSocket](https://img.shields.io/badge/WebSocket-010101?style=flat)

---

## 📂 프로젝트 목록

### 🔵 Circle 0
| 프로젝트 | 설명 | 기술 |
|---------|------|------|
| [**libft**](./circle_0/libft) | C 표준 라이브러리 함수 직접 구현 (40+ 함수, 연결 리스트 포함) | `C` |

---

### 🟢 Circle 1
| 프로젝트 | 설명 | 기술 |
|---------|------|------|
| [**born2beroot**](./circle_1/born2beroot) | Debian 가상 머신 구축 및 서버 보안 설정 | `Linux` `VM` `bash` |
| [**ft_printf**](./circle_1/ft_printf) | printf 함수 재구현 — 가변인수 & 형식 지정자 파싱 | `C` `stdarg` |
| [**get_next_line**](./circle_1/get_next_line) | fd에서 한 줄씩 읽는 함수 구현 — 정적 변수 & 버퍼 관리 | `C` |

---

### 🟡 Circle 2
| 프로젝트 | 설명 | 기술 |
|---------|------|------|
| [**minitalk**](./circle_2/minitalk) | UNIX 시그널만으로 구현한 IPC 통신 프로그램 | `C` `SIGUSR1/2` |
| [**push_swap**](./circle_2/push_swap) | 두 스택을 이용한 정렬 알고리즘 (Greedy + Deque) | `C` |
| [**so_long**](./circle_2/so_long) | 2D 탑뷰 게임 — 맵 파싱, 이동, 수집 요소 구현 | `C` `MiniLibX` |

---

### 🟠 Circle 3
| 프로젝트 | 설명 | 기술 |
|---------|------|------|
| [**minishell**](./circle_3/minishell) | Bash 셸 구현 — 토크나이저, 파서, 실행기, 파이프라인 | `C` `fork/exec` `readline` |
| [**philosophers**](./circle_3/philosophers) | 식사하는 철학자 문제 — 멀티스레드 데드락 방지 | `C` `pthreads` `mutex` |

---

### 🔴 Circle 4
| 프로젝트 | 설명 | 기술 |
|---------|------|------|
| [**netpractice**](./circle_4/netpractice) | TCP/IP 네트워킹 기초 — 서브넷 계산과 라우팅 설계 | `네트워킹` |
| [**cub3d**](./circle_4/cub3d) | DDA 레이캐스팅 기반 3D 렌더링 엔진 | `C` `MiniLibX` `수학` |
| [**cpp (00~04)**](./circle_4/cpp) | C++ 기초 — 클래스, 상속, 다형성, 추상화, 인터페이스 | `C++` `OOP` |

---

### 🟣 Circle 5
| 프로젝트 | 설명 | 기술 |
|---------|------|------|
| [**cpp (05~09)**](./circle_5/cpp) | C++ 심화 — 예외처리, 형변환, 템플릿, STL 컨테이너 | `C++` `STL` `Templates` |
| [**ft_irc**](./circle_5/ft_irc) | RFC 기반 IRC 서버 구현 — 멀티클라이언트, 채널 관리 | `C++` `socket` `epoll` |
| [**inception**](./circle_5/inception) | Docker로 구성한 LEMP 스택 (Nginx, WordPress, MariaDB) | `Docker` `Nginx` `MariaDB` |

---

### ⚫ Circle 6 — 최종 프로젝트
| 프로젝트 | 설명 | 기술 |
|---------|------|------|
| [**ft_transcendence**](./circle_6/ft_transcendence) | 실시간 멀티플레이어 웹 게임 플랫폼 (팀 프로젝트, TL 담당) | `React` `TypeScript` `Fastify` `WebSocket` `Docker` |

---

## 🏆 하이라이트 프로젝트

<table>
<tr>
<td width="33%" valign="top">

### 🎮 ft_transcendence
**실시간 멀티플레이어 웹 플랫폼**

5인 팀 프로젝트에서 **Technical Lead** 담당.  
React + TypeScript 프론트엔드 아키텍처 설계,  
WebSocket 기반 게임 룸 UI 구현,  
팀 코드 컨벤션 및 브랜치 전략 수립.

`React` `TypeScript` `Fastify` `Prisma` `WebSocket` `Docker`

[📁 자세히 보기](./circle_6/ft_transcendence)

</td>
<td width="33%" valign="top">

### 🐚 minishell
**Bash 셸 직접 구현**

lexer → tokenizer → parser → executor  
파이프라인(`|`), 리디렉션(`>`, `<`, `>>`),  
환경변수 확장, 시그널 처리, 빌트인 명령어  
(cd, echo, export, unset, env, exit) 구현.

`C` `fork/exec` `dup2` `readline`

[📁 자세히 보기](./circle_3/minishell)

</td>
<td width="33%" valign="top">

### 🎯 cub3d
**레이캐스팅 3D 엔진**

Wolfenstein-style 3D 렌더러를  
수학적으로 구현한 그래픽 프로젝트.  
DDA 알고리즘, 텍스처 매핑,  
벽/바닥/천장 렌더링, 이벤트 루프 처리.

`C` `MiniLibX` `선형대수` `DDA`

[📁 자세히 보기](./circle_4/cub3d)

</td>
</tr>
</table>

---

## 📈 커먼코어 진행 현황

```
Circle 0  ████████████████████  libft
Circle 1  ████████████████████  born2beroot · ft_printf · get_next_line
Circle 2  ████████████████████  minitalk · push_swap · so_long
Circle 3  ████████████████████  minishell · philosophers
Circle 4  ████████████████████  netpractice · cub3d · cpp00~04
Circle 5  ████████████████████  cpp05~09 · ft_irc · inception
Circle 6  ████████████████████  ft_transcendence ✅ COMPLETED
```

---

## 💡 배운 것들

| 분야 | 핵심 학습 내용 |
|------|--------------|
| **메모리 관리** | malloc/free, 메모리 누수 방지, Valgrind 디버깅 |
| **시스템 프로그래밍** | 프로세스, 시그널, 파일 디스크립터, IPC |
| **멀티스레딩** | POSIX 스레드, 뮤텍스, 데드락 방지, 경쟁 조건 |
| **네트워킹** | TCP/IP, 소켓 프로그래밍, 비동기 I/O |
| **OOP / C++** | 클래스, 상속, 다형성, 예외처리, STL, 템플릿 |
| **웹 & 풀스택** | REST API, WebSocket, JWT 인증, ORM, Docker |
| **인프라** | Docker Compose, 리버스 프록시, HTTPS, CI/CD |

---

## 📬 Contact

- **42 Gyeongsan:** djang
- **GitHub:** [github.com/djang](https://github.com/djang) ← *링크 직접 수정*
- **Email:** ← *이메일 추가*
