# C++ Modules (05~09)

> 42 Gyeongsan — Circle 5

C++ 심화 개념을 다루는 모듈 시리즈입니다.  
예외 처리, 형변환, 제네릭 프로그래밍(템플릿), STL 컨테이너를 단계적으로 학습합니다.

---

## 모듈별 핵심 주제

| 모듈 | 주제 | 핵심 내용 |
|------|------|----------|
| **cpp05** | 예외 처리 | `try`/`catch`/`throw`, 커스텀 예외 클래스, 중첩 예외 |
| **cpp06** | 형변환 | `static_cast`, `dynamic_cast`, `reinterpret_cast`, `const_cast` |
| **cpp07** | 템플릿 | 함수 템플릿, 클래스 템플릿, 특수화 |
| **cpp08** | STL 컨테이너 | `vector`·`list`·`deque`·`stack`·`map`, 반복자(iterator) |
| **cpp09** | STL 심화 | `std::sort`, `std::find`, 함수 객체, 병합 정렬 구현 |

---

## 상세 내용

### cpp05 — 예외 처리
```cpp
class GradeTooHighException : public std::exception {
    const char* what() const throw() {
        return "Grade is too high!";
    }
};

try {
    bureaucrat.incrementGrade();
} catch (std::exception &e) {
    std::cerr << e.what() << std::endl;
}
```

### cpp06 — C++ 형변환
```cpp
double d = 3.14;
int i = static_cast<int>(d);           // 컴파일타임 안전 변환

Animal *a = new Dog();
Dog *d = dynamic_cast<Dog*>(a);        // 런타임 타입 안전 다운캐스트
```

### cpp07 — 제네릭 프로그래밍
```cpp
template <typename T>
T max(T a, T b) { return (a > b) ? a : b; }
```

### cpp08 — STL 컨테이너

| 컨테이너 | 특징 |
|---------|------|
| `vector` | 동적 배열, 임의 접근 O(1) |
| `list` | 이중 연결 리스트, 삽입/삭제 O(1) |
| `deque` | 양방향 큐 |
| `map` | 레드-블랙 트리, 검색 O(log n) |

### cpp09 — Ford-Johnson 정렬
- `std::sort`, `std::find`, `std::remove_if` 실전 사용
- Merge-Insertion Sort 직접 구현

---

## 배운 점

- C++ RAII 패턴과 예외 안전성(Exception Safety) 설계
- 정적/동적 형변환의 차이와 안전한 사용 시나리오
- 템플릿으로 타입에 독립적인 재사용 가능 코드 작성
- STL 컨테이너와 반복자(iterator) 패턴 실전 적용
- 알고리즘 복잡도와 컨테이너 선택의 트레이드오프
