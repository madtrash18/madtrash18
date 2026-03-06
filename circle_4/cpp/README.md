# C++ Modules (00~04)

> 42 Gyeongsan — Circle 4

C++의 객체지향 프로그래밍(OOP) 핵심 개념을 단계적으로 학습하는 모듈 시리즈입니다.

---

## 모듈별 핵심 주제

| 모듈 | 주제 | 핵심 내용 |
|------|------|----------|
| **cpp00** | C++ 기초 | 네임스페이스, 클래스, 멤버 함수, stdio 스트림, 초기화 리스트 |
| **cpp01** | 메모리 관리 | 힙/스택 할당, 포인터 vs 레퍼런스, 파일 스트림, `new`/`delete` |
| **cpp02** | 연산자 오버로딩 | Orthodox Canonical Form, 고정소수점 클래스, 연산자/비교 오버로딩 |
| **cpp03** | 상속 | 클래스 상속, 다중 상속, 다이아몬드 문제, 가상 기반 클래스 |
| **cpp04** | 다형성 | 순수 가상 함수, 추상 클래스, 인터페이스, 깊은 복사/얕은 복사 |

---

## 상세 내용

### cpp00 — 네임스페이스와 클래스
- C에서 C++로의 전환: `::`, `std::cout`, `std::string`
- 클래스 기초: 생성자, 소멸자, 접근 제어자 (`public`/`private`)
- 멤버 함수와 const 멤버

### cpp01 — 포인터와 레퍼런스
```cpp
int &ref = var;   // 레퍼런스: 별칭, 재할당 불가
int *ptr = &var;  // 포인터: 주소 저장, 재할당 가능
```
- `new`/`delete`로 힙 메모리 관리

### cpp02 — Orthodox Canonical Form
모든 클래스가 갖춰야 할 4가지:
```cpp
class Fixed {
public:
    Fixed();
    Fixed(const Fixed &src);
    Fixed &operator=(const Fixed &rhs);
    ~Fixed();
};
```

### cpp03 — 상속과 다이아몬드
```
        Animal
       /      \
    ClapTrap  ...
    /    \
ScavTrap FragTrap
    \    /
   DiamondTrap  ← virtual 상속으로 해결
```

### cpp04 — 추상화와 인터페이스
```cpp
class AAnimal {
    virtual void speak() = 0;  // 순수 가상 함수
};
```

---

## 배운 점

- OOP의 4대 원칙: 캡슐화, 상속, 다형성, 추상화
- C와 C++의 메모리 관리 차이 (`malloc` vs `new`)
- 연산자 오버로딩으로 자연스러운 타입 설계
- 가상 함수와 vtable을 이용한 런타임 다형성
- 다중 상속과 가상 기반 클래스로 다이아몬드 문제 해결
