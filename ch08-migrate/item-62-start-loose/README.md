# TL;DR

- 자바스크립트에서 타입스크립트로 마이그레이션하기 위해 `noImplicitAny` 설정을 활성화 해야합니다.
- `noImplicitAny` 설정이 없다면 타입 선언과 관련된 실제 오류가 드러나지 않습니다.
- `noImplicitAny`과 같이 엄격한 타입 체크를 설정하는 경우 로컬에서부터 설정하여 타입 오류를 점진적으로 수정해야 합니다.
- 엄격한 타입 체크를 적용하기 전 팀원들이 타입스크립트에 익숙해질 수 있도록 합니다.

![item62_발표자료_이보리-1](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/a950468a-e2bf-44d2-9ffe-bef0967a5295)

![item62_발표자료_이보리-2](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/4b4f2c7a-92e8-4c76-a63b-d7008af648fd)

![item62_발표자료_이보리-3](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/1c5b4490-9f4c-4fb1-94e8-c267311d2d72)

![item62_발표자료_이보리-4](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/f7cceb93-89fc-4c6f-9176-73e495f303d2)

![item62_발표자료_이보리-5](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/a5571cf0-0613-434d-aa44-0e40a3e46e1d)

![item62_발표자료_이보리-6](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/9461fc09-81a3-4cee-8b31-7da82c5cf3ab)

![item62_발표자료_이보리-7](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/05ee26be-9e3f-4ce0-94d3-0792d77b65c4)

![item62_발표자료_이보리-8](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/1d693995-d048-4848-83dc-5a46b531dcac)
