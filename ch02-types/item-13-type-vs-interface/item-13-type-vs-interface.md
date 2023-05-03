# 타입과 인터페이스의 차이점 알기 | Effective TypeScript

## 명명된 타입 정의하기

타입스크립트에서 명명된 타입(named type)을 정의하는 방법은 두 가지가 있습니다.

1. 타입 별칭(type alias) : `type` 키워드를 사용하여 타입 정의
2. 인터페이스(interface) : `interface` 키워드를 사용하여 타입 정의

```typescript
// 1. Type alias
type Person = {
  name: string;
  gender: string;
}

// 2. Interface
interface Person {
  name: string;
  gender: string;
}
```

## 인터페이스 선언과 타입 별칭 선언

명명된 타입은 인터페이스로 정의하든 타입 별칭으로 정의하든 상태에는 차이가 없습니다.

### 공통점
#### 1. 잉여 속성 체크
`type Person`와 `interface Person`를 추가 속성과 함께 할당하면 다음과 같이 잉여 속성 체크가 수행되며 동일한 오류가 발생합니다.

![](https://i.imgur.com/I6LROQI.png)

#### 2. 인덱스 시그니처
인터페이스와 타입 별칭에서 인덱스 시그니처를 사용할 수 있습니다.

![](https://i.imgur.com/sVDxrUz.png)

#### 3. 함수 타입 정의
인터페이스와 타입 별칭으로 함수 타입을 정의할 수 있습니다.

![](https://i.imgur.com/832I3iG.png)

함수 타입에 추가적인 속성이 있다면 다음과 같이 작성할 수 있습니다.

![](https://i.imgur.com/h7nkxBL.png)

#### 4. 제너릭
인터페이스와 타입 별칭에서 제너릭이 가능합니다.

![](https://i.imgur.com/5fOpJai.png)

#### 5. 타입 확장
인터페이스는 타입 별칭을 확장할 수 있고, 타입 별칭은 인터페이스를 확장할 수 있습니다.
따라서, 인터페이스와 타입 별칭은 서로 확장 가능합니다.

![](https://i.imgur.com/9wuylP7.png)

#### 6. 클래스 구현(implements)
클래스를 구현할 때 타입 별칭과 인터페이스 모두 사용할 수 있습니다.

![](https://i.imgur.com/qcU4WKN.png)

### 차이점

#### 1. 타입 확장
타입 별칭은 유니온 타입, 매핑된 타입(mapped type), 조건부 타입(conditional type) 과 같은 고급 기능을 활용하여 복잡한 타입을 표현할 수 있습니다.

![](https://i.imgur.com/5wuuUez.png)

반면, 인터페이스는 유니온 또는 인터섹션 할 수 없습니다. 따라서, 타입을 확장할 수 있지만 복잡한 타입을 확장하지 못합니다.

![](https://i.imgur.com/XOubcMc.png)

#### 2. 튜플과 배열 타입
`type` 키워드를 이용하여 튜플과 배열 타입을 정의할 수 있습니다.

![](https://i.imgur.com/r82g9Ae.png)

다음과 같이 인터페이스로도 튜플과 비슷하게 구현할 수 있으나, `concat` 같은 튜플의 메서드를 사용할 수 없습니다.
따라서, 튜플은 `type` 키워드로 구현하는 것이 좋습니다.

![](https://i.imgur.com/Quv5X2u.png)

#### 3. 인터페이스의 선언 병합(declaration merging)
"선언 병합"은 컴파일러가 같은 이름으로 선언된 개별적인 선언 두 개를 하나의 정의로 합치는 것을 의미합니다.
인터페이스는 다음과 같이 선언 병합을 이용한 보강(augment)이 가능합니다.

![](https://i.imgur.com/oVmDbpy.png)

따라서, 타입 별칭은 기존 타입에 추가적인 보강이 필요 없는 경우에만 사용해야 합니다.

## 마무리
타입을 정의는 타입 별칭과 인터페이스 두 가지 방법으로 할 수 있습니다. 두 문법의 공통점과 차이점을 이해하고 작성 방법을 터득해야 합니다.
프로젝트에 따라 어떤 문법을 사용할 지 결정할 때 일관된 스타일을 확립하고, 확장이 필요한지 고려해야 합니다.

> #### 참고
> - [The TypeScript Handbook](https://www.typescriptlang.org/ko/docs/handbook/intro.html)
> - [interface vs type alias](https://tecoble.techcourse.co.kr/post/2022-11-07-typeAlias-interface/)
> - [[TS] type과 interface 당신의 선택은?](https://velog.io/@turtle601/TS-type%EA%B3%BC-interface-%EB%8B%B9%EC%8B%A0%EC%9D%98-%EC%84%A0%ED%83%9D%EC%9D%80)
