# 타입과 인터페이스의 차이점 알기 | Effective TypeScript

## 명명된 타입 정의하기

타입스크립트에서 명명된 타입(named type)을 정의하는 방법은 두 가지가 있습니다.

#### 1. 인터페이스(interface)
- 객체의 구조를 정의하는 방법 중 하나입니다.
- 객체의 필드와 메소드를 선언하고, 이를 구현한 클래스나 객체가 인터페이스의 규약을 따르도록 강제하여 일관성을 유지할 수 있도록 합니다.
- `interface` 키워드를 사용하여 타입을 정의합니다.

![](https://i.imgur.com/XjCpxMc.png)

#### 2. 타입 별칭(type alias)
- 원시 타입이나 유니언 타입, 튜플 등등 모든 변수에 자유롭게 활용할 수 있는 커스텀 타입을 의미합니다.
- 기존에 존재하는 타입에 새로운 이름을 부여하여 복잡한 타입을 단순하게 줄여서 사용할 수 있습니다.
- `type` 키워드를 사용하여 타입을 정의합니다.

![](https://i.imgur.com/eqYnGw0.png)


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
하지만 제한 사항이 있습니다. 자세한 내용은 두 문법의 차이점에서 설명하겠습니다.

![](https://i.imgur.com/9wuylP7.png)

#### 6. 클래스 구현(implements)
클래스를 구현할 때 타입 별칭과 인터페이스 모두 사용할 수 있습니다.
과거 타입 별칭은 `implements` 를 사용할 수 없었으나 현재 변경되어 사용할 수 있게 되었습니다.

![](https://i.imgur.com/qcU4WKN.png)

### 차이점

#### 1. 타입 확장

인터페이스는 `extends` 키워드 사용하여 상속을 통한 타입 확장을 할 수 있습니다.

![](https://i.imgur.com/rK3ggnw.png)

하지만 유니온 또는 인터섹션을 사용할 수 없어 복잡한 타입은 표현할 수 없습니다.

![](https://i.imgur.com/XOubcMc.png)

반면, 타입 별칭은 `extends` 키워드를 통해 타입을 확장할 수 없었지만, 2.7 버전부터 인터섹션 타입의 등장으로 `&` 기호를 이용하여 타입을 결합할 수 있습니다.

![](https://i.imgur.com/8koCURP.png)

또한 유니온 타입, 매핑된 타입(mapped type), 조건부 타입(conditional type) 과 같은 고급 기능을 활용하여 복잡한 타입을 표현할 수 있습니다.

![](https://i.imgur.com/5wuuUez.png)

#### 2. 튜플과 배열 타입
`type` 키워드를 이용하여 튜플과 배열 타입을 정의할 수 있습니다.

![](https://i.imgur.com/r82g9Ae.png)

다음과 같이 인터페이스로도 튜플과 비슷하게 구현할 수 있으나, `concat` 같은 튜플의 메서드를 사용할 수 없습니다.
따라서, 튜플은 `type` 키워드로 구현하는 것이 좋습니다.

![](https://i.imgur.com/Quv5X2u.png)

#### 3. 인터페이스의 선언 병합(declaration merging)
"선언 병합"은 컴파일러가 같은 이름으로 선언된 개별적인 선언 두 개를 하나의 정의로 합치는 것을 의미합니다.
인터페이스는 다음과 같이 선언 병합을 이용한 보강(augment)이 가능하지만 타입 별칭은 불가능합니다.

![](https://i.imgur.com/oVmDbpy.png)

따라서, 외부에 노출해야 하는 public API에서 타입은 인터페이스를 통해 정의하는 것이 좋습니다. API가 변경될 때 사용자가 인터페이스를 통해 새로운 필드를 병합하여 사용할 수 있기 때문입니다.
그러나 프로젝트 내부적으로 사용되는 타입에 선언 병합이 발생하는 것은 잘못된 설계입니다.

타입 별칭으로 정의된 타입은 조금 더 제한적이기 때문에 private API 같이 외부에 노출할 필요가 없거나 프로젝트 내부적으로 사용되는 타입을 정의할 때는 타입 별칭을 사용하는 것이 좋습니다.


## 마무리
타입을 정의는 타입 별칭과 인터페이스 두 가지 방법으로 할 수 있습니다. 두 문법은 비슷한 역할을 하지만 명확한 차이점이 있습니다.

인터페이스는 선언 병합을 통한 확장성이 좋습니다. 따라서 일반적으로는 인터페이스를 사용하고, 유니온이나 튜플과 같은 타입이 필요한 경우에만 타입 별칭을 사용하는 것이 좋습니다.
TypeScript 공식 문서에서도 특별한 상황이 아니라면 인터페이스 사용을 권장하고 있습니다.

프로젝트에서 어떤 문법을 사용할 지 결정해야할 때 한 가지 일관된 스타일을 확립하고, 확장이 필요한지 고려해야 합니다.

> #### 참고
> - [The TypeScript Handbook](https://www.typescriptlang.org/ko/docs/handbook/intro.html)
> - [interface vs type alias](https://tecoble.techcourse.co.kr/post/2022-11-07-typeAlias-interface/)
> - [[TS] type과 interface 당신의 선택은?](https://velog.io/@turtle601/TS-type%EA%B3%BC-interface-%EB%8B%B9%EC%8B%A0%EC%9D%98-%EC%84%A0%ED%83%9D%EC%9D%80)
> - [TypeScript - Interface](https://poiemaweb.com/typescript-interface)
> - [타입스크립트에서 타입 별칭과 인터페이스의 차이 알기](https://funes-days.com/dev/difference-of-type-alias-and-interface-in-typescript)
> - [TypeScript에서 Type을 기술하는 두 가지 방법, Interface와 Type Alias](https://joonsungum.github.io/post/2019-02-25-typescript-interface-and-type-alias/)
