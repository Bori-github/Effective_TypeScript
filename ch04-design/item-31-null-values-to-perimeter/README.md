# TL;DR
- strictNullChecks는 `null`과 `undefined` 값을 엄격하게 다루는 TypeScript 컴파일러의 옵션 중 하나입니다.
- strictNullChecks 옵션을 켜면 `null`이나 `undefined` 값 관련된 오류들이 나타나기 때문에 `null`과 `undefined`에 대한 명확한 처리 로직이 필요합니다.
- 이를 통해 `null` 값과 관련된 문제점을 찾을 수 있고, `null` 값에 대한 처리를 명확하게 할 수 있어 코드의 안정성을 높일 수 있습니다.
- 여러 개의 변수에 대한 null 값을 체크할 경우 각 변수를 체크하는 것보다 하나의 객체에 넣어 사용하면 코드가 간결해지고 `null` 체크가 용이해집니다.

![item31_발표자료_이보리-1](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/ab3ffd67-0721-4fe7-9a20-34ae826f09c5)

![item31_발표자료_이보리-2](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/d00eca0c-94e7-47d1-bc9a-c1aec1ec860f)

![item31_발표자료_이보리-3](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/7c0b4606-e5c0-4114-8d78-45d333f7b3a6)

![item31_발표자료_이보리-4](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/5ca006c0-e6a9-4592-9331-84a56ab6323d)

![item31_발표자료_이보리-5](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/d2f7aacb-0038-4fad-91ae-a4b1e01f704f)

![item31_발표자료_이보리-6](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/9efbda8b-7449-46d1-9dbe-ec1052c82b90)

![item31_발표자료_이보리-7](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/46d0b302-9220-4625-a53b-6a4097ff3d87)

![item31_발표자료_이보리-8](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/45ea1e6e-9930-431b-bb05-3472e077c299)
