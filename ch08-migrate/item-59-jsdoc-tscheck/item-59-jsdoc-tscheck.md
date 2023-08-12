# 타입스크립트 도입 전에 `@ts-check`와 JSDoc으로 시험해 보기 | Effective TypeScript

타입스크립트로 전환하기 전에 `@ts-check` 지시자를 사용하여 타입스크립트 전환 시 어떤 문제가 발생하는지 미리 시험해볼 수 있습니다.

## `@ts-check`

`@ts-check` 지시자를 허용하면 타입 체커가 파일을 분석하고, 발견된 오류를 보고하도록 지시합니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/e2c52e62-4ffe-4f91-820d-7658555a8418)

하지만 매우 느슨한 수준의 타입 체크를 수행한다는 점을 주의해야합니다.

> #### `noImplicitAny` 설정
>
> 명시되지 않은 타입을 컴파일러가 추론할 때 any로 추론하게 되면 컴파일 에러로 나타내는 기능입니다.
> `@ts-check` 지시자는 `noImplicitAny` 설정을 해제한 것보다 느슨한 체크를 수행합니다.

`@ts-check` 지시자를 사용했을 때 나타날 수 있는 몇가지 오류에 대해 알아봅시다.

## 선언되지 않은 전역 변수

선언된 변수가 어딘가에 숨어있다면, 변수를 제대로 인식할 수 있게 타입 선언 파일을 만들어야 합니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/a12fb148-85c7-4622-b1f6-d6f26c906d7c)

`user` 를 다음과 같이 `types.d.ts`라는 타입 선언 파일을 만들면 오류가 해결됩니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/6b97d5f8-2fa2-4d1d-a6de-33a5f940884d)

만약 타입 선언 파일을 찾지 못한다면, 트리플 슬래시 참조(`///`)를 사용하여 명시적으로 임포트할 수 있습니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/e4b2c7cb-cd70-4b7e-ab0a-71ef2dea2ad4)

## 알 수 없는 라이브러리

서드파티 라이브러리를 사용하는 경우, 서드파티 라이브러리의 타입 정보를 알아야 합니다.
라이브러리를 사용하는 코드에 `@ts-check` 지시자를 사용하면 오류가 발생합니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/4a019e46-c0d4-42af-a4ac-53589fc6a160)

먼저, 라이브러리 타입 선언 패키지를 설치하여 타입 정보를 알아냅니다.
타입 선언 패키지 설치 후에도 오류가 남아있다면 이는 해당 라이브러리의 사양과 관련된 오류이므로 적절한 속성을 사용하여 오류를 해결할 수 있습니다.

## DOM 문제

타입스크립트는 DOM 엘리먼트 관련된 부분에서 많은 오류를 표시합니다.

`HTMLxxxElement` 형태의 특정 DOM 엘리먼트들은 자신만의 고유한 속성을 가지고 있고, 이런 속성에 접근하려면 실제 엘리먼트의 구체적인 타입을 지정해야합니다.

만약 `getElementById` 와 같이 요소의 정보를 알 수 없는 경우 정확한 타입을 얻을 수 없기 때문에 고유한 속성에 접근할 때 오류가 발생합니다.
이는 타입 단언으로 해결할 수 있으나 자바스크립트 파일에서는 사용할 수 없습니다.

대신 JSDoc을 사용하여 타입 단언을 대체할 수 있습니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/8e2a7cb7-f776-48ff-a183-f86dc19b6547)

JSDoc의 `@type `구문을 사용할 때 타입을 감싸는 중괄호가 필요합니다.

## 부정확한 JSDoc

프로젝트에서 이미 JSDoc을 사용하고 있다면, `@ts-check` 지시자를 설정하는 순간 기존 주석에 타입 체크가 동작합니다.

JSDoc이 부정확하여 타입이 일치하지 않는 경우 오류가 발생합니다.
이는 JSDoc에 작성된 잘못된 타입을 올바른 타입으로 수정하여 해결합니다.

JSDoc을 활용하면 타입 정보를 점진적으로 추가할 수 있습니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/018637d7-6069-4bc9-806c-6f7d9ca61cec)

`double` 함수의 매개변수에 마우스 커서를 올리면 위와 같은 메시지가 나타나면서 빠른 수정이라는 버튼이 나타납니다. 빠른 수정을 실행하면 타입 정보가 자동으로 JSDoc 주석으로 생성됩니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/8a05c16d-1c18-4805-8389-0dfb3579d3cf)

하지만 잘 동작하지 않는 경우도 있으니 자동 생성 기능을 사용할 경우 추가적인 확인이 필요합니다.

이를 통해 자바스크립트 환경에서 `@ts-check` 지시자와 JSDoc을 이용하여 타입스크립트와 비슷한 경험으로 작업을 해보았습니다.
`@ts-check` 지시자와 JSDoc을 장기간 사용하는 것은 많은 주석이 늘어나 로직을 해석하는데 방해가 될 수 있기 때문에 좋지 않습니다.

마이그레이션의 궁극적인 목표는 자바스크립트에 JSDoc 주석이 있는 형태가 아니라 모든 코드가 타입스크립트 기반으로 전환되는 것이라는 것을 잊지 말아야 합니다.

## 마무리

- 파일 상단에 `@ts-check` 지시자를 추가하여 자바스크립트에서도 타입 체크를 수행할 수 있습니다.
- JSDoc 주석을 잘 활용하면 자바스크립트에서도 타입 단언과 타입 추론을 할 수 있습니다.
- JSDoc 주석은 마이그레이션의 중간 단계 이기 때문에 너무 공들이지 않도록 합니다. 최종 목표는 `.ts`로 된 타입스크립트 코드임을 잊지 말아야 합니다.
