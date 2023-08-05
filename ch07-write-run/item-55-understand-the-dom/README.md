# TL;DR

- 타입스크립트에서는 DOM 엘리먼트이 계층 구조를 파악하기 용이합니다.
- DOM에는 타입 계층 구조가 있고, 타입스크립트에서 DOM 타입은 중요한 정보입니다.
- Element와 EventTarget에 달려있는 Node의 구체적인 타입을 안다면 타입 오류를 디버깅할 수 있고, 언제 타입 단언을 사용해야 할지 알 수 있습니다.
- DOM 계층 구조의 각 타입간의 차이점과 이벤트 타입의 차이점을 알아야 고유의 속성을 에러없이 사용할 수 있습니다.
- DOM 엘리먼트와 이벤트에는 구체적인 타입 정보를 사용하거나, 타입스크립트가 추론할 수 있도록 문맥 정보를 활용해야 합니다.

![item55_발표자료_이보리-01](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/8562e85a-8403-4f66-b9b0-a21ade5aef67)

![item55_발표자료_이보리-02](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/d2592865-6549-4dae-9475-056a05bb613d)

![item55_발표자료_이보리-03](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/deb0a177-57aa-4224-9723-949da3317dc9)

![item55_발표자료_이보리-04](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/9149179b-905b-46bf-94b3-6d91673c78fa)

![item55_발표자료_이보리-05](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/af27535f-679d-4e10-b723-b8fcb9f60ec6)

![item55_발표자료_이보리-06](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/0044337a-7e71-435b-878b-43d3ad496373)

![item55_발표자료_이보리-07](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/a14f2c28-0d5a-4a70-a068-11e63c11f0fc)

![item55_발표자료_이보리-08](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/047280f3-0ce8-44bb-affb-dcf6f7c5539f)

![item55_발표자료_이보리-09](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/8a6641b1-8dc1-4cb9-9e29-a0f7824de570)

![item55_발표자료_이보리-10](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/2a6c2960-fe09-4196-8108-44d9941c7b72)

![item55_발표자료_이보리-11](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/96a6fb23-8f98-46ba-a259-76bb09d846ab)

![item55_발표자료_이보리-12](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/f090067f-34cb-4d2e-807c-89050bbae480)

![item55_발표자료_이보리-13](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/b70c896f-eb40-41b4-8cb0-a69b270f6948)

![item55_발표자료_이보리-14](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/1b997a98-80fe-4d28-9b99-9c7f1e4aca1b)

![item55_발표자료_이보리-15](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/fb587c58-274a-4abe-9260-b26c52be4341)

![item55_발표자료_이보리-16](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/2caf6a14-b83e-4886-94e7-ecd00b517d7d)

![item55_발표자료_이보리-17](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/5516c6b7-2347-4d9a-95f9-38c532bf5dcb)

![item55_발표자료_이보리-18](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/6240b04b-5bea-4ef9-a4f1-6d55e4cea137)
