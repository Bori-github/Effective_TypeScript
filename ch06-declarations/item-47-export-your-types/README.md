# TL;DR
- 자바스크립트로 만들어진 서드 파티 라이브러리를 타입스크립트에서 사용하려면 각 기능에 대한 타입이 정의되어 있어야 합니다.
- 라이브러리를 사용하다보면 익스포트(export)되지 않은 타입 정보가 필요한 경우가 발생하기도 합니다.
이 때 타입 간 매핑을 해주는 도구를 사용하거나 필요한 타입을 참조하는 방법을 사용할 수 있습니다.
- `Parameters`/`ReturnType` 제네릭 타입 등을 사용하여 숨겨진 타입을 추출할 수 있습니다.
- 따라서, 라이브러리 사용자가 타입을 추출할 수 있으므로, 익스포트하기 쉽게 모든 타입은 익스포트 하는 것이 좋습니다.

![item47_발표자료_이보리-1](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/e1635263-597d-4c45-87c5-5c97cf88bbad)

![item47_발표자료_이보리-2](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/3f145f33-6115-44c8-9044-fa11c10944a5)

![item47_발표자료_이보리-3](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/c3a51720-702b-48fc-8db7-85e976a6f8a1)

![item47_발표자료_이보리-4](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/8fecbccb-f7d1-478e-b4ed-8df512aa9f32)

![item47_발표자료_이보리-5](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/83c31a81-3fb6-4bef-b633-552328aa7572)

![item47_발표자료_이보리-6](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/c8ea5f93-f180-47cb-ae55-e86c65d8c6e6)

![item47_발표자료_이보리-7](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/0d8de97a-7df9-4842-ba72-539b499fe9ef)

![item47_발표자료_이보리-8](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/5f013f3d-8f13-4c04-8c50-24e3e4b708e2)
