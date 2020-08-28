---
layout: post
title: 협업을 위한 코드 작성법
category: git
tags: [git, code]
comments: true
---

# 언어마다 컨벤션이 있다.

# 어떻게 해야 읽기 좋은 코드가 될까?

- 누가 봐도 읽기 좋은 코드가 되어야 한다.

### 이름 짓는 방법

- 언어마다 naming convention이 존재한다. 카멜케이스로 표기하되 클래스의 맨 앞문자는 대문자로 표기하고 변수, 삼수등은 소문자로 표기하는 등의 통용되는 규칙들이 존재한다.

- 1.의도가 분명한 이름을 짓는다. 역할이 분명해야한다.

- 1-1) 줄여쓰지 않는다.
- 잘 알려진 축약어(ex> CPU, for문에 i와 j)를 제외하고 축약어를 쓰지 말것(ex> comp는 compare을 의미하는지 computer를 의미하는지 모른다.)

- 1-2) 애매한 단어를 쓰지 않는다.
- process 처리하다의 경우 무엇을 처리하는지 정확하지 않다. 무엇을 처리하는지 다른 단어를 쓰자.
- 유틸리티성 클래스는 추상적인 단어를 써도 적절하다.

- 1-3) 메소드의 경우 리턴값을 포함해서 이름을 짓는다.
- `return 'Empty' OR return list.get(0)`인 경우 getFirstElementorEmpty로 명시한다.

- 1-4) 단어의 뜻을 고류해서 이름을 짓는다.
- getX()는 존재한는 값을 가져올 때 쓴다. 없으면 에러가 뜬다. 반면, findY()는 찾아보고 없어도 된다.
- initialize()는 객체의 상태를 최초로 설정한다. 반면, create()는 새 객체를 생성한다.

- 1-5) 단어의 이름은 통일되게 짓는다
- 한 패키지에서 AuthenticationProvider로 지었다면 패키지 안의 클래스에서는 NotificationProvide로 짓는다.
- productInfo, productData, productSummary로 나눠서 짓지 않는다.

- 1-6) 함수는 동사로 시작하고 목적어가 될 명사를 붙인다.
- boolean을 반환 하는 함수는 is, exists, has, use등으로 시작한다.
- boolean을 반환하는 함수는 긍정문으로 작성하자(if(isPossible()))


### 함수 작성법

- 1-1) 함수를 작게 만들기
- 함수를 작게 만들수록 가독성과 유지보수에 좋다.
- 유지 보수성을 위해서는 코드의 길이를 **15줄 이내**로 작성하자.
- **수평방향 스크롤**도 고려해서 개행하자.

- 1-2) 입력 형식에 대해서 제한을 둔다.
- 입력값을 검사하는 코드가 짧아진다.

- 1-3) 함수 내부도 추상화하라
- validateAndReport(){}메소드의 내부는 `validate(); report();`여야한다.
- `Reporter report = new Reporter(); report.report();`처럼 객체를 생성해서 메소드를 사용하지 말자.

- 1-4) 중괄호는 중첩을 피하자
- 메서드당 들여쓰기는 깊이가 한 단계 이상 넘어가지 말아야 한다.
- 이중 for문을 쓰는 경우 안의 포문은 다른 메소드로 대체하자.

```java
// 변경 전
for(int i=0; i<VERTICAL_SIZE; i++){
    for(int j=0; j<HORIZONTAL_SIZE; j++){
        showCell(i, j);
    }
}

// 변경 후
for(int i=0; i<VERTICAL_SIZE; i++){
    showLine(i);
}
```

- 1-5) 매개변수의 개수는 줄이자
- 매개변수가 많으면 가독성을 크게 저하시킨다.

- 1-6) 인자 유효성검사는 하자
- 함수 인자에 대해서는 유효성을 철저히 해야한다. 그러나 불필요한 검사나 중복 검사는 피해야한다.

