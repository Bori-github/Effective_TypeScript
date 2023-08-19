# 마이그레이션의 완성을 위해 noImplicitAny 설정하기 | Effective TypeScript

## `noImplicitAny`

자바스크립트에서 타입스크립트로 마이그레이션하기 위해 모든 파일을 `.ts`로 전환한 후 추가적인 설정이 필요합니다.

`noImplicitAny`를 설정하는 것입니다.

```json
// tsconfig.json
{
  "compilerOptions": {
    "noImplicitAny": true,
    ...
  }
}
```

`noImplicitAny`는 TypeScript 컴파일러 옵션 중 하나로, 타입을 명시적으로 지정하지 않아 컴파일 시 암묵적으로 `any`로 추론되는 경우 오류를 표시합니다.

`noImplicitAny`를 설정하지 않았을 경우 어떤 문제가 발생하는지 알아봅시다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/7a3bda0a-5490-4a04-a199-f68c6b96523d)

`for of`문을 이용해 숫자 배열인 `indices`를 순회합니다.
이 때 `index`는 숫자로 추론됩니다.
`for of`문 내부에서 `row`와 `column`을 선언하고 각각 `index[0]`, `index[1]`을 할당합니다.
`index`는 숫자 타입이기 때문에 인덱스로 접근할 수 없지만 아무런 오류가 발생하지 않습니다.

이처럼 타입 체크가 매우 허술합니다.

`noImplicitAny`를 설정하면 다음과 같은 오류가 발생합니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/b738d51d-5723-490c-97ac-1f011b53f811)

`index`는 숫자 타입이므로 인덱스를 통해 접근할 수 없다는 오류가 발생합니다.

## 타입 체크 강도 높이기

처음에는 `noImplicitAny`를 로컬에만 설정하여 빌드 시 문제가 발생하지 않도록 하는 것이 좋습니다. 로컬에서만 오류로 인식되기 때문에 타입 오류를 점진적으로 수정하는 것이 가능합니다.

타입 체크 강도를 높이는 설정에는 여러 가지가 있습니다.

`strictNullChecks`는 `null`과 `undefined`를 명시적으로 다루도록 강제하는 설정입니다.
`strictNullChecks`를 설정하면 모든 타입에 `null`과 `undefined`를 할당할 수 없지만 유니온 타입으로 명시한다면 할당할 수 있습니다.
기본적으로 any에는 `null`과 `undefined`를 할당할 수 있고, `void`에는 `undefined`를 할당할 수 있습니다.

`strict`는 가장 강력한 설정으로 타입스크립트의 각종 타입 체크를 전부 활성화합니다.

```json
// tsconfig.json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    ...
  }
}
```

타입 체크의 강도는 팀 내의 모든 사람이 타입스크립트에 익숙해진 다음에 조금씩 높이는 것이 좋습니다.

## 마무리

- `noImplicitAny` 설정을 활성화하여 마이그레이션의 마지막 단계를 진행해야 합니다. `noImplicitAny` 설정이 없다면 타입 선언과 관련된 실제 오류가 드러나지 않습니다.
- `noImplicitAny`를 전면 적용하기 전에 로컬에서부터 타입 오류를 점진적으로 수정해야합니다. 엄격한 타입 체크를 적용하기 전 팀원들이 타입스크립트에 익숙해질 수 있도록 합니다.

> #### 참고
>
> - [컴파일러 옵션 (Compiler Options)](https://typescript-kr.github.io/pages/compiler-options.html)
> - [타입스크립트 컴파일 설정 - tsconfig 옵션 총정리](https://inpa.tistory.com/entry/TS-%F0%9F%93%98-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-tsconfigjson-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0-%EC%B4%9D%EC%A0%95%EB%A6%AC)
