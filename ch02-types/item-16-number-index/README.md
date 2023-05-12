# TL;DR
- 자바스크립트의 객체 키는 문자열이나 심벌만 가능합니다. 숫자는 사용할 수 없습니다.
- 자바스크립트의 배열은 객체입니다. 숫자 인덱스로 배열의 요소에 접근할 수 있는 이유는 자바스크립트 엔진이 숫자 인덱스를 암묵적 타입 변환을 통해 문자열로 변환하기 때문입니다.
- 인덱스 시그니처로 사용된 숫자 타입은 타입 체크 시점의 버그를 잡기 위한 순수 타입스크립트 코드입니다. 실제로 런타임에는 키가 문자열로 변환된다는 것을 이해하고 사용해야 합니다.
- 숫자 타입을 인덱스 시그니처에 사용하는 것보다 이미 정의되어 있는 Array, 튜플, ArrayLike 타입을 사용하는 것이 좋습니다.

![item16_발표자료_이보리-1](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/dc945247-c3c1-4d78-84b4-5baf35a09416)

![item16_발표자료_이보리-2](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/17178364-519f-45f7-87ad-f8425eec9f6a)

![item16_발표자료_이보리-3](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/22222be0-1f78-4a14-a1fe-b6f7942d606f)

![item16_발표자료_이보리-4](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/431f2e2f-61eb-4b99-bb73-8d63be6371d9)

![item16_발표자료_이보리-5](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/296ece59-f2e5-44df-90a1-d5f7a49454ec)

![item16_발표자료_이보리-6](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/d2087e0f-3f66-4b2b-88cc-2da5166777a9)

![item16_발표자료_이보리-7](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/bb685e67-982a-4252-b90d-66d0a3c56304)

![item16_발표자료_이보리-8](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/2855b982-b939-4742-8c9a-4a242c9ea3d7)
