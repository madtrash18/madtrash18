# ft_printf

> 42 Gyeongsan — Circle 1

C 표준 라이브러리의 `printf` 함수를 직접 재구현한 프로젝트입니다.  
가변인수(`va_list`)와 형식 지정자(format specifier) 파싱 로직을 직접 설계하고 구현했습니다.

---

## 지원하는 형식 지정자

| 지정자 | 설명 |
|--------|------|
| `%c` | 단일 문자 |
| `%s` | 문자열 |
| `%p` | 포인터 주소 (16진수) |
| `%d` / `%i` | 부호 있는 정수 |
| `%u` | 부호 없는 정수 |
| `%x` / `%X` | 16진수 (소문자 / 대문자) |
| `%%` | 리터럴 `%` 출력 |

---

## 구현 방식

```
ft_printf(const char *format, ...)
│
├── va_start() 로 가변인수 리스트 초기화
├── format 문자열을 순회
│   ├── '%' 발견 시 → 다음 문자로 지정자 파악
│   └── 일반 문자 → 그대로 출력
└── 각 지정자에 맞는 출력 함수 호출
    ├── ft_putchar, ft_putstr
    ├── ft_putnbr (base 10)
    └── ft_puthex (base 16)
```

---

## 빌드

```bash
make        # libftprintf.a 빌드
make clean
make fclean
make re
```

---

## 배운 점

- `stdarg.h`의 `va_list`, `va_start`, `va_arg`, `va_end` 사용법
- 형식 문자열 파싱 패턴 설계
- 진수 변환 알고리즘 (10진수 ↔ 16진수)
- 출력 값을 반환(출력된 글자 수 카운트)하는 누적 합산 패턴
