# libft

> 42 Gyeongsan — Circle 0

C 표준 라이브러리의 핵심 함수들을 직접 구현한 개인 라이브러리입니다.  
이후 모든 42 과제의 기반이 되는 첫 번째 프로젝트입니다.

---

## 구현 함수 목록

### Part 1 — libc 재구현

| 함수 | 설명 |
|------|------|
| `ft_isalpha` / `ft_isdigit` / `ft_isalnum` | 문자 분류 |
| `ft_isascii` / `ft_isprint` | ASCII 범위 검사 |
| `ft_toupper` / `ft_tolower` | 대소문자 변환 |
| `ft_strlen` | 문자열 길이 계산 |
| `ft_memset` / `ft_bzero` / `ft_memcpy` / `ft_memmove` | 메모리 조작 |
| `ft_memchr` / `ft_memcmp` | 메모리 탐색 및 비교 |
| `ft_strlcpy` / `ft_strlcat` | 안전한 문자열 복사/이어붙이기 |
| `ft_strchr` / `ft_strrchr` | 문자 탐색 |
| `ft_strncmp` / `ft_strnstr` | 문자열 비교/탐색 |
| `ft_atoi` | 문자열 → 정수 변환 |
| `ft_calloc` / `ft_strdup` | 메모리 할당 |

### Part 2 — 추가 함수

| 함수 | 설명 |
|------|------|
| `ft_substr` | 부분 문자열 추출 |
| `ft_strjoin` | 두 문자열 연결 |
| `ft_strtrim` | 양쪽 공백(지정 문자) 제거 |
| `ft_split` | 구분자로 문자열 분리 → 배열 반환 |
| `ft_itoa` | 정수 → 문자열 변환 |
| `ft_strmapi` / `ft_striteri` | 함수 적용 매핑 |
| `ft_putchar_fd` / `ft_putstr_fd` / `ft_putendl_fd` / `ft_putnbr_fd` | fd 출력 |

### Bonus — 연결 리스트

| 함수 | 설명 |
|------|------|
| `ft_lstnew` | 새 노드 생성 |
| `ft_lstadd_front` / `ft_lstadd_back` | 앞/뒤 삽입 |
| `ft_lstsize` / `ft_lstlast` | 크기/마지막 노드 |
| `ft_lstdelone` / `ft_lstclear` | 노드 삭제 |
| `ft_lstiter` / `ft_lstmap` | 순회/변환 |

---

## 빌드

```bash
make        # libft.a 빌드
make bonus  # 연결 리스트 포함
make clean  # 오브젝트 파일 제거
make fclean # 라이브러리까지 제거
make re     # 클린 후 재빌드
```

---

## 배운 점

- `malloc` / `free`를 통한 수동 메모리 관리의 기초
- 포인터 연산과 배열의 관계를 깊이 이해
- Makefile 작성 및 정적 라이브러리(`ar`) 생성 방법
- 테스트 주도적 개발: 엣지 케이스 (NULL, 빈 문자열, 경계값) 처리
