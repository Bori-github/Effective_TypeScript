# 타입 공간과 값 공간의 심벌 구분하기 | Effective TypeScript

타입스크립트의 *심벌(symbol)은 타입 공간이나 값 공간 중 한 곳에 존재합니다.
같은 이름의 심벌이라도 어느 공간에 속하느냐 따라 다른 것을 나타낼 수 있습니다.

##### *심벌 : 본 내용에서 식별자를 의미

![](https://i.imgur.com/jUiOvQ9.png)

- `interface Cylinder`에서 Cylinder는 **타입**으로 쓰입니다.
- `const Cylinder`에서 Cylinder는 `interface Cylinder`와 이름이 같지만 **값**으로 쓰입니다.
- 서로 아무런 관련이 없고 상황에 따라 Cylinder는 타입으로 쓰일 수도 있고, 값으로 쓰일 수도 있습니다.

이런 점이 아래와 같은 오류를 발생시킵니다.

![](https://i.imgur.com/bNrxnp7.png)

- `instanceof`를 이용하여 `shape`이 Cylinder 타입인지 체크합니다.
- 그러나 `instanceof`는 런타임 연산자이고, 값에 대해 연산하므로 `instanceof Cylinder`는 타입이 아닌 함수를 참조하며 오류가 발생합니다.

따라서 타입스크립트 코드를 읽을 떄 타입인지 값인지 구분하는 방법을 터득해야 합니다.

## 타입 공간과 값 공간
#### 타입과 값의 구분
- 일반적으로 `type`이나 `interface` 다음에 오는 심벌은 **타입**입니다.
- `const`, `let`으로 선언된 심벌은 **값**입니다.
- 변수나 함수를 선언하면 "값 공간"에 선언되고, 타입을 선언하면 "타입 공간"에 선언됩니다.

#### 타입 공간(type space)
- 타입이 들어가는 공간으로 타입스크립트가 자바스크립트로 변환되면 사라집니다.(class, enum은 예외)


#### 값 공간(value space)
- string, number, object 등 구체적인 값이 들어가는 공간으로 타입스크립트가 자바스크립트로 변환되어도 유지됩니다.

![](https://i.imgur.com/K24JZ4Y.png)
- 위의 그림은 타입스크립트 플레이그라운드에서 자바스크립트로 변환된 코드입니다.
- T1, T2 심벌은 컴파일 과정에서 제거된 것을 보여주고, 이 두 심벌은 타입에 해당하는 것을 알 수 있습니다.

위의 내용에서 타입스크립트의 심벌은 타입 공간이나 값 공간 중 한 곳에 존재한다고 하였습니다.
하지만 타입 공간과 값의 공간에 동시에 존재하는 것이 있습니다.

#### `class`와 `enum`은 상황에 따라 타입과 값 두 가지 모두 가능한 예약어입니다.

- `class`나 `enum`은 값 공간과 타입 공간 모두에 속하며, 타입이기도 하면서 인스턴스를 만드는 생성자 함수이기도 합니다.

![](https://i.imgur.com/4XmIPzs.png)

- `class`가 타입으로 쓰일 때는 형태(속성과 메서드)가 사용되는 반면, 값으로 쓰일 때는 생성자가 사용됩니다.

## 타입 공간과 값 공간에서 다른 의미를 가지는 코드 패턴

### `typeof` 연산자
- 연산자 중 `typeof` 연산자는 타입에서 쓰일 때와 값에서 쓰일 때 다른 기능을 합니다.

#### 타입의 관점에서 `typeof`
- 값을 읽어서 타입스크립트 타입을 반환합니다.
- 이 때 `typeof`는 보다 큰 타입의 일부분으로 사용할 수 있고, `typeof` 구문으로 이름을 붙이는 용도로 사용할 수 있습니다.

#### 값의 관점에서 `typeof`
- 자바스크립트 런타임의 `typeof` 연산자로 동작합니다.
- 대상 심벌의 런타임 타입을 가리키는 문자열을 반환합니다.

#### `class`에 대한 `typeof`의 동작
![](https://i.imgur.com/YyImX2B.png)

- `class`는 자바스크립트에서 실제 함수로 구현되므로 `const v` 값은 "function"이 되고, `type T`의 타입은 "typeof Cylinder"가 됩니다.

### `this`
- 값으로 쓰이는 `this`는 자바스크립트의 `this` 키워드 입니다.
- 타입으로 쓰이는 `this`는 ['다형성(polymorphic) this'](https://typescript-kr.github.io/pages/advanced-types.html#%EB%8B%A4%ED%98%95%EC%84%B1-this-%ED%83%80%EC%9E%85-polymorphic-this-types)라고 불리는 `this`의 타입스크립트 타입입니다.

### `&`와 `|`
- 값에서 `&`와 `|`는 AND와 OR 비트 연산입니다.
- 타입에서는 [인터섹션 타입](https://typescript-kr.github.io/pages/advanced-types.html#%EA%B5%90%EC%B0%A8-%ED%83%80%EC%9E%85-intersection-types)과 [유니온 타입](https://typescript-kr.github.io/pages/advanced-types.html#%EC%9C%A0%EB%8B%88%EC%96%B8-%ED%83%80%EC%9E%85-union-types) 입니다.

### `const`
- `const`는 새 변수를 선언하지만 `as const`는 리터럴 또는 리터럴 표현식의 추론된 타입을 바꿉니다.

### `extends`
- `extends`는 [서브클래스(`class A extends B`)](https://typescript-kr.github.io/pages/classes.html), [서브타입(`interface A extends B`)](https://typescript-kr.github.io/pages/interfaces.html), [제네릭 타입의 한정자(`Generic<T extends number>`)](https://typescript-kr.github.io/pages/generics.html)를 정의할 수 있습니다.

### `in`
- `in`은 루프(`for (key in object)`) 또는 [매핑된 타입(mapped type)](https://typescript-kr.github.io/pages/advanced-types.html#%EB%A7%A4%ED%95%91-%ED%83%80%EC%9E%85-mapped-types)에 등장합니다.

## 요약
- 타입스크립트 코드를 읽을 때 타입인지 값인지 구분하는 방법을 터득해야 합니다.
- `type`과 `interface`같은 키워드는 타입 공간에만 존재합니다.
- `class`와 `enum` 키워드는 타입과 값 두 가지로 사용될 수 있습니다.
- `typeof`, `this` 등 연산자들과 키워드들은 타입 공간과 값 공간에서 다른 목적으로 사용될 수 있습니다.

> #### 참고
> - [타입스크립트에서 타입](https://lunatk.github.io/2021/02/07/20210207-type-in-typescript/)
> - [타입 공간과 값 공간의 심벌 구분](https://junghyunkim.tistory.com/entry/%EC%9D%B4%ED%8E%99%ED%8B%B0%EB%B8%8C-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B88-%ED%83%80%EC%9E%85-%EA%B3%B5%EA%B0%84%EA%B3%BC-%EA%B0%92-%EA%B3%B5%EA%B0%84%EC%9D%98-%EC%8B%AC%EB%B2%8C-%EA%B5%AC%EB%B6%84)
> - [TypeScript-Handbook 한글 문서](https://typescript-kr.github.io/)