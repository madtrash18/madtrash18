# ft_irc

> 42 Gyeongsan — Circle 5

RFC 1459 기반의 **IRC(Internet Relay Chat) 서버**를 C++로 구현한 네트워크 프로그래밍 프로젝트입니다.  
실제 IRC 클라이언트(irssi, HexChat 등)와 연동하여 동작합니다.

---

## 핵심 기능

| 기능 | 상세 |
|------|------|
| **소켓 서버** | TCP 소켓, 비동기 I/O (`poll`) |
| **멀티클라이언트** | 단일 스레드로 여러 클라이언트 동시 처리 |
| **채널 관리** | 채널 생성/참여/퇴장, 채널별 멤버 관리 |
| **오퍼레이터** | 채널 오퍼레이터 권한, KICK/INVITE/TOPIC/MODE |
| **IRC 명령어** | 표준 IRC 프로토콜 명령어 파싱 및 처리 |

---

## 구현한 IRC 명령어

| 명령어 | 설명 |
|--------|------|
| `PASS` | 연결 비밀번호 인증 |
| `NICK` | 닉네임 설정 |
| `USER` | 사용자 등록 |
| `JOIN` | 채널 참여 |
| `PART` | 채널 퇴장 |
| `PRIVMSG` | 개인/채널 메시지 전송 |
| `KICK` | 채널에서 사용자 강퇴 |
| `INVITE` | 채널 초대 |
| `TOPIC` | 채널 주제 설정/조회 |
| `MODE` | 채널 모드 설정 (i/t/k/o/l) |
| `QUIT` | 서버 연결 종료 |

---

## 동작 방식

```
[클라이언트 연결]
      │
      ▼
[poll()로 이벤트 감지]   ← 단일 스레드 비동기 I/O
      │
      ├─ 새 연결 (accept)
      ├─ 데이터 수신 → IRC 메시지 파싱 → 명령어 핸들러 실행
      └─ 연결 종료 감지 → 채널에서 해당 사용자 제거
```

---

## 실행 방법

```bash
make
./ircserv [port] [password]

./ircserv 6667 passwd42

# irssi 클라이언트 연결
/connect localhost 6667 passwd42
/join #42gyeongsan
```

---

## 소스 구조

```
includes/
  ├── Server.hpp
  ├── Client.hpp
  ├── Channel.hpp
  └── Command.hpp

srcs/
  ├── Server.cpp
  ├── Client.cpp
  ├── Channel.cpp
  └── commands/
```

---

## 배운 점

- TCP 소켓 프로그래밍: `socket`, `bind`, `listen`, `accept`, `recv`, `send`
- `poll()`을 이용한 단일 스레드 논블로킹 I/O 멀티플렉싱
- RFC 규격에 맞는 프로토콜 파싱 및 응답 코드 처리
- 채널/클라이언트 상태 관리와 메모리 안전한 C++ 설계
