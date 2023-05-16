# 다른 타입에는 다른 변수 사용하기 | Effective TypeScript

## 변수 재사용
자바스크립트에서는 한 변수를 다른 목적을 가지는 다른 타입으로 재사용할 수 있습니다.

![](https://hackmd.io/_uploads/r1_q8dlrh.png)

위 예제에서 `fetchProduct`는 `string` 타입의 `id`를 매개변수 가지고, `fetchProductBySerialNumber`는 `number` 타입의 `id`를 매개변수 가집니다.

`let` 키워드로 선언된 변수 `id`는 `string` 타입의 값이 할당되어 있습니다.

그리고 `id`에 `number` 타입의 값을 재할당하고, `fetchProductBySerialNumber`에 인수로 전달하면 타입스크립트에서는 두 가지 오류를 나타냅니다.

1. `id`는 "12-23-56"이라는 값을 통해 `string`으로 추론되어 `number` 타입을 재할당할 수 없습니다.
  ⇒ 7번째 줄 `id`에서 오류 발생
2. `string`으로 추론된 `id`를 `number` 형식의 매개변수에 할당할 수 없습니다.
  ⇒ 8번째 줄 `id`에서 오류 발생

이를 통해 "**변수의 값은 바뀔 수 있지만 그 타입은 보통 바뀌지 않는다**"는 관점을 알 수 있습니다.
타입을 바꿀 수 있는 방법 중 하나는 범위를 좁히는 것입니다(아이템 22에서 자세히 다룹니다).

## 타입 좁히기

위 예제의 `id`에 `string`과 `number`를 모두 포함할 수 있도록 유니온 타입을 사용하여 확장해보겠습니다.

![](https://hackmd.io/_uploads/SJ85qOeS3.png)

유니온 타입 사용으로 타입스크립트는 `fetchProduct`에서 `id`는 `string`으로, `fetchProductBySerialNumber`에서 `id`는 `number`로 판단합니다.
하지만, `id`를 사용할 때마다 값이 어떤 타입인지 확인해야하기 때문에 그에 따른 문제가 발생할 수 있습니다.

## 다른 변수 사용하기

사실 위의 예제에서 첫 번째 `id`와 두 번째 `id`는 변수를 재사용 했을 뿐 서로 관련이 없습니다.
변수를 무분별하게 재사용한다면 타입 체커와 사람 모두에게 혼란을 줍니다.
따라서, 다른 타입에는 별도의 변수를 사용하는 것이 바람직합니다.

![](https://hackmd.io/_uploads/BJpklFxr2.png)

다른 변수를 사용하면 다음과 같은 장점이 있습니다.

- 서로 관련이 없는 두 개의 값 분리
- 구체적인 변수명
- 타입 추론 향상 및 불필요한 타입 구문 제거
- 간결한 타입 정의
- `let` 대신 `const` 키워드를 사용한 변수 선언

이 때 주의할 점은 재사용되는 변수와 **가려지는 변수**를 혼동해서는 안됩니다.

> #### 가려지는 변수(Variable shadowing)
> Variable shadowing은 하나의 범위(scope) 내에서 동일한 이름의 변수가 중복해서 선언되는 현상으로 외부 범위에서 이미 선언된 변수와 동일한 이름의 변수가 내부 범위에서 선언되면, 내부 범위에서의 변수가 외부 범위에서의 변수를 "가리게" 되는 것을 의미합니다.

다음 코드는 가려지는 변수로 인해 타입의 오류가 발생하지 않습니다.

![](https://hackmd.io/_uploads/SJg9gteB3.png)

## 마무리
- 변수의 값은 바뀔 수 있지만 타입은 일반적으로 바뀌지 않습니다.
- 타입이 다른 값을 다룰 때에는 변수를 재사용하는 것보다 다른 변수를 선언하여 사용하는 것이 바람직합니다.

> #### 참고
> - [scope chain 과 variable shadowing에 대해](https://all-dev-kang.tistory.com/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-scope-chain-%EA%B3%BC-variable-shadowing%EC%97%90-%EB%8C%80%ED%95%B4)