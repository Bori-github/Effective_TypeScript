# TL;DR
- 몽키 패치란 런타임 중인 프로그램의 내용이 변경되는 것을 의미합니다.
- JavaScript는 선언시점이 아닌 사용시점에 객체와 클래스에 임의의 속성을 추가하여 사용할 수 있습니다.
- 몽키 패치를 사용할 경우 의도치 않은 객체에도 속성이 추가되거나 전역 변수가 적용되어 사이드 이펙트를 고려해야하는 등의 문제점이 발생할 수 있습니다.
- 따라서, 몽키 패치를 남용하지 않도록 구조를 설계하는 것이 좋습니다.
- 내장 타입에 데이터를 저장해야 하는 경우, 보강 기능을 이용하거나 내장 타입을 확장하여 타입 단언을 적용하는 방법과 같은 안전한 타입 접근법을 사용해야 합니다.
- 보강 기능을 사용할 경우 모듈의 영역 문제를 이해하고 사용해야 합니다.

![item43_발표자료_이보리-01](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/87c757ea-0518-4654-aafc-b3b17585ed9f)

![item43_발표자료_이보리-02](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/89f32638-f872-4e54-aaca-0d3cbd857c68)

![item43_발표자료_이보리-03](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/89cb4f73-d7b4-455e-a730-9335d3652ebb)

![item43_발표자료_이보리-04](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/342a2912-65a9-4cb5-9c23-9b0570a919a6)

![item43_발표자료_이보리-05](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/eda9c0ae-545c-408d-8a1b-c0c368fa23d7)

![item43_발표자료_이보리-06](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/330bafa4-88e2-46cb-8ae0-f1cdddf0ba06)

![item43_발표자료_이보리-07](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/9e1cb7cd-9982-4c4a-8b27-37b1144bfd97)

![item43_발표자료_이보리-08](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/14c5f481-31e3-464d-b1ca-7fd2a5a25158)

![item43_발표자료_이보리-09](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/f0400060-f74d-4ad9-9e0a-fe05068e33ea)

![item43_발표자료_이보리-10](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/bd01c574-ab7b-475d-8f13-8f5fce7c4abc)

