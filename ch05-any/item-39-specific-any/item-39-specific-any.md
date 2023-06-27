## any 타입
***`any`* 타입은 자바스크립트에서 표현할 수 있는 모든 값을 아우르는 큰 범위의 타입** 모든 숫자, 문자열, 배열, 객체, 정규식, 함수, 클래스, DOM 앨리먼트, `null`, `undefined`가 포함됩니다.
일반적인 상황에서는 `any` 보다 더 구체적으로 표현할 수 있는 타입이 존재할 가능성이 높습니다.
따라서, 타입의 안정성을 높이기 위해 보다 구체적인 타입을 사용해야 합니다.

## any 타입 구체적으로 사용하기

예제를 통해 any 타입 구체적으로 사용해봅시다!

### 배열 타입 구체적으로 사용하기

![img1](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/1bc90eea-9785-4059-944d-0e52db10d95f)

`getLengthBad` 함수는 `any` 타입의 array를 매개변수를 받습니다.
`getLength` 함수는 `any[]` 타입의 array를 매개변수를 받습니다.

매개변수로 `any` 타입을 사용한 것과 `any[]` 타입을 사용한 것은 큰 차이점이 있습니다.

![Group 143](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/68a98ec4-7c83-44b3-b6b4-8d9dfb0744ce)

`any[]` 타입을 사용하면 다음과 같은 장점이 있습니다.
- 매개변수가 배열인지 체크합니다.
- 함수 내의 array.length 타입이 체크됩니다.
- 함수의 반환 타입이 any 대신 number로 추론됩니다.

`any` 타입을 사용하는 것보다 타입의 안정성을 높일 수 있습니다.

### 객체 타입 구체적으로 사용하기

만약 함수의 매개변수가 객체이지만 값을 알 수 없다면 어떤 타입을 사용하는 것이 좋을까요?

`object` 타입을 사용할 수 있습니다.
`object` 타입은 객체의 키를 열거할 수 있지만 속성에 접근할 수 없어 다음과 같은 에러가 발생합니다.

![Group 142](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/fb8d56cb-1760-4734-b877-d535e280e421)

TypeScript는 기본적으로 객체의 속성을 읽을 때, `string` 타입의 키를 허용하지 않습니다. 객체의 속성을 읽기 위해서는 반드시 `string literal` 타입이 키로 접근해야 합니다.

객체의 속성에 접근해야 한다면, `string` 타입의 키를 허용하기 위해 `object` 타입 대신 인덱스 시그니처를 사용하여 `{[key: string]: any}` 타입을 사용할 수 있습니다.

![img3](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/63769327-cc60-4ba3-9138-64a9a6ff9109)

### 함수 타입 구체적으로 사용하기

함수의 타입에도 단순한 any 타입을 사용하는 것보다 구체화해서 사용해봅시다.

```typescript
// 매개변수 없이 호출 가능한 모든 함수
type Fn = () => any;

// 매개변수가 1개인 함수
type FnWithArg = (arg: any) => any;

// 매개변수가 여러 개인 함수
type FnWithArgs = (...arg: any[]) => any;
```

> `FnWithArgs` 타입은 위의 "배열 타입 구체적으로 사용하기"의 예제를 참고해주세요:)

## 마무리
- `any` 타입은 모든 타입을 허용하기 때문에 사용하기 전에 정말로 모든 값이 허용되어야 하는지 검토해야합니다.
- 타입의 안정성을 높이기 위해 단순한 `any` 타입을 사용하는 것보다 위의 예제와 같이 구체적인 형태를 사용해야 합니다.

> 참고
> - [TypeScript에서 string key로 객체에 접근하기](https://soopdop.github.io/2020/12/01/index-signatures-in-typescript/)