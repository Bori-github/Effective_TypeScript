# TL;DR

- 파일 상단에 `@ts-check` 지시자를 추가하여 자바스크립트에서도 타입 체크를 수행할 수 있습니다.
- JSDoc 주석을 잘 활용하면 자바스크립트에서도 타입 단언과 타입 추론을 할 수 있습니다.
- 자바스크립트 환경에서 `@ts-check` 지시자와 JSDoc을 이용하여 타입스크립트와 비슷한 경험으로 작업할 수 있습니다.
- `@ts-check` 지시자와 JSDoc을 장기간 사용하는 것은 많은 주석이 늘어나 로직을 해석하는데 방해가 될 수 있기 때문에 좋지 않습니다. 또한 JSDoc 주석은 마이그레이션의 중간 단계 이기 때문에 너무 공들이지 않도록 합니다.
- 최종 목표는 모든 코드가 타입스크립트 기반으로 전환되는 것이라는 것을 잊지 말아야 합니다.

![item59_발표자료_이보리-01](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/f9167155-55f1-4d43-8c38-888f671cb3dd)

![item59_발표자료_이보리-02](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/4935d579-d9db-42e6-9441-5a435e4c428b)

![item59_발표자료_이보리-03](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/99883661-fe38-4687-988b-fdeff2952bde)

![item59_발표자료_이보리-04](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/e3428ffa-8eae-488d-8b59-795d9c4e583b)

![item59_발표자료_이보리-05](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/b2a4bc7c-2c13-4b89-a87b-15d393ede345)

![item59_발표자료_이보리-06](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/f9ecf3c1-3010-46af-b756-e9bbaf479d7d)

![item59_발표자료_이보리-07](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/e106f99e-f432-4835-870c-ec49aa1a6f64)

![item59_발표자료_이보리-08](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/eedb2d43-c8d2-4b64-af1f-fcdddd464b38)

![item59_발표자료_이보리-09](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/a6bf71d9-858b-4b59-a29a-8d874054c12e)

![item59_발표자료_이보리-10](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/fde2c427-42b6-4b8e-b531-0bd9d386f0ff)

![item59_발표자료_이보리-11](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/9bc51a91-4aba-4110-8da8-a223fb268a2c)

![item59_발표자료_이보리-12](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/808d188d-d220-4c7b-8688-d6f5012fb587)
