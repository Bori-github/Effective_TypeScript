# TL;DR

- 공개 라이브러리를 작성할 경우, 다른 라이브러리의 타입에 의존할 수 있습니다.
- 여러 사용자를 고려하여 공개 라이브러리를 사용하는 여러 그룹의 사용자가 각자 사용하지 않는 모듈의 의존성을 가지지 않게 해야합니다.
- 다른 라이브러리의 타입에만 의존하는 경우, 필요한 선언부만 추출하여 작성 중인 라이브러리에 넣는 **미러링(mirroring)** 을 적용할 수 있습니다.
- 만약 다른 라이브러리의 타입 선언의 대부분을 추출해야한다면, 미러링 대신 명시적으로 `@type` 의존성을 추가하는 것이 좋습니다.

![item51_발표자료_이보리-1](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/fe5e7431-a6da-4336-8d32-da5747f4320f)

![item51_발표자료_이보리-2](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/38221dd8-78a1-4361-829d-a224d92af8d8)

![item51_발표자료_이보리-3](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/66adb398-a07b-4682-beba-0c87c9efc32e)

![item51_발표자료_이보리-4](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/be60c9a9-6446-4f88-ae9d-ea18001d303a)

![item51_발표자료_이보리-5](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/ff327c57-67b7-4c66-9c00-58ea65ade074)

![item51_발표자료_이보리-6](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/2475f917-62ab-42ad-93dd-30d7e57be445)

![item51_발표자료_이보리-7](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/11afd7bf-b0ea-442d-bb1f-841fca292a97)

![item51_발표자료_이보리-8](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/e066debb-46fb-40ea-aea9-aa64e7cd931e)
