# 타입 주변에 null 값 배치하기 | Effective TypeScript

## strictNullChecks 란?

TypeScript 컴파일러의 옵션 중 하나로 `null`과 `undefined` 값을 엄격하게 다룹니다. 따라서, strictNullChecks 옵션을 켜면 `null`이나 `undefined` 값 관련된 오류들이 나타나게 됩니다.

strictNullChecks 옵션을 사용하면 다음과 같은 장점이 있습니다.
- 변수 또는 매개변수에 `null` 또는 `undefined`를 할당할 수 없습니다. 값이 예상되는 곳에서 오류를 사전에 방지할 수 있기 때문에 타입 안정성이 향상됩니다.
- `null` 또는 `undefined`를 실수로 다른 값과 혼동하여 사용하는 것을 방지합니다.
- `null`과 `undefined`의 사용을 명시적으로 처리해야하기 때문에 코드의 의도를 명확히 알 수 있습니다.

따라서, strictNullChecks 옵션을 사용시 `null`과 `undefined`에 대한 명확한 처리 로직이 필요합니다.

## strictNullChecks 옵션 사용하기

숫자들의 최솟값과 최댓값을 계산하는 `extent` 함수 코드입니다.

![](https://user-images.githubusercontent.com/85009583/243955352-add77ad4-d16b-4b5e-96a2-b65944378ede.png)

최솟값과 최댓값을 저장할 변수 `min`, `max`를 선언합니다.
숫자 배열 `nums`를 순회하면서, `min` 값이 존재하지 않는 경우 즉 첫 번째 숫자인 경우, 현재 숫자를 `min`과 `max`에 할당합니다.
그렇지 않은 경우 현재 값과 `min`, `max` 값을 비교하여 재할당합니다.
숫자 배열의 순회가 끝나면 최솟값과 최대값을 배열로 묶어 반환합니다.

이 코드에는 **문제점**이 있습니다.

1. 변수 `min`, `max`는 타입이 명시되어 있지 않습니다.
⇒ 두 변수는 **`undefined`로 초기화**되고, 타입은 **any**로 추론됩니다.
2. `if (!min)`은 `null`만 체크하고 `undefined`에 대해서는 동작하지 않을 수 있습니다.
3. `!min`은 **모든 falsy 값을 처리**합니다. 숫자 배열을 다루는 함수이기 때문에 배열 요소에 0이 포함되어 있다면, if문 내의 코드가 실행되면서 의도하지 않은 결과를 반환할 수 있습니다.
```typescript
// 숫자 배열 내 0이 포함되어 있는 경우
const [min, max] = extent([0, 1, 2]);
console.log(min, max); // [1, 2] => 의도치 않은 결과 반환
```
> #### truthy와 falsy
> - 자바스크립트는 제어문의 조건식과 같은 불리언 값으로 평가되어야 하는 컨텍스트에서 불리언 값이 아닌 값을 암묵적으로 불리언 값으로 변환합니다.
> - `true`로 변환되는 값을 **truthy**, `false`로 변환되는 값을 **falsy**라고 합니다.
> - falsy 값 : false, undefined, null, 0, -0, NaN, 빈 문자열
4. 변수 `max` 값은 체크하고 있지 않습니다.

![](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/98992de9-b4b2-401c-b48d-95b394a57f3b)


이러한 문제점들로 인해 `extent`의 반환 타입은 `(number | undefined)[]`로 추론되어, `extent`를 호출하는 곳마다 타입 오류가 발생합니다.

위의 문제를 해결하기 위해 두 변수에 타입을 명시적으로 지정하거나, 초기값을 할당할 수 있습니다.
이런 방식의 경우 각 변수에 대한 체크가 필요합니다.

![](https://user-images.githubusercontent.com/85009583/243955367-9089ee48-5afb-4b41-b977-858c1fa38d93.png)


## 값이 전부 null 이거나 전부 null 이 아닌 경우로 구분하기

조금 더 나은 방법은 **두 변수를 하나의 객체에 넣어** `null` 체크를 하는 것입니다.

![](https://user-images.githubusercontent.com/85009583/243955345-70dbff5e-0251-4383-a94a-b7c5c8542a57.png)

1. 변수 `result`에 타입을 명시적으로 지정하고 `null`로 초기화 했습니다.
2. `if (!result)`에서 `undefined`에 대한 고려를 하지 않아도 됩니다.
3. 함수 `extent`의 반환 타입이 `[number, number] | null`으로 명확해졌습니다.

`extent`의 결과값으로 단일 객체를 사용하여 설계를 개선하고, 타입스크립트가 `null` 값 사이의 관계를 이해할 수 있도록 하여 버그를 제거했습니다.

## 마무리
- strictNullChecks 옵션을 사용하면 `null` 값과 관련된 문제점을 찾을 수 있고, `null` 값에 대한 처리를 명확하게 할 수 있어 코드의 안정성을 높일 수 있습니다.
- 코드 설계 시 한 값의 `null` 여부가 다른 값의 `null` 여부를 암시적으로 관련되도록 설계하면 안됩니다.
- 변수의 타입을 지정하고, 초기값을 할당하여 `null` 체크를 명시적으로 할 수 있도록 합니다.
- 여러 개의 변수를 하나의 객체에 넣어 사용하면 코드가 간결해지고 `null` 체크가 용이해집니다.

> #### 참고
> - [TSConfig Option: strictNullChecks - TypeScript](https://www.typescriptlang.org/tsconfig#strictNullChecks)
> - [엄격하게 타입스크립트를 이용하는 9가지 방법](https://velog.io/@baby_dev/%EC%97%84%EA%B2%A9%ED%95%98%EA%B2%8C-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%98%EB%8A%94-9%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95#6-null%EA%B3%BC-undefined%EB%8A%94-%ED%99%95%EC%8B%A4%ED%95%98%EA%B2%8C-%EC%B2%B4%ED%81%AC%ED%95%98%EC%9E%90)