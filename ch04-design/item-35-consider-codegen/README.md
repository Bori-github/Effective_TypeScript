# TL;DR
- 코드의 타입 안정성을 얻기 위해 파일 형식, API, 명세 등 프로젝트 외부에서 비롯된 타입은 명세를 참고해 타입을 생성해야 합니다.
- 예시 데이터를 참고하여 타입을 생성하면 데이터에 드러나지 않는 예외적인 경우들이 문제가 될 수 있기 때문에 데이터보다는 명세로부터 타입을 생성하는 것이 좋습니다.
- GraphQL은 API를 위한 쿼리 언어로, 타입스크립트와 비슷한 타입 시스템을 사용합니다.Apollo와 같은 GraphQL 쿼리를 타입스크립트 타입으로 변환해주는 도구를 이용하여 스키마로부터 특정 쿼리의 타입스크립트 타입을 생성할 수 있고, API를 문서화할 수 있습니다.
- 만약 명세 정보나 공식 스키마가 없다면 데이터로부터 타입을 생성해주는 도구인 quicktype을 사용할 수 있습니다. quicktype은 JSON 데이터를 분석하여 해당 데이터에 대한 타입 정의를 생성해주지만 생성된 타입이 실제 데이터와 일치하지 않을 수 있다는 점을 주의해야 합니다.

![item35_발표자료_이보리-1](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/684d0354-fe6e-4368-9be3-43511ab579b8)

![item35_발표자료_이보리-2](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/b7898dbb-8a6e-437b-9ca3-ac82ce5ff79f)

![item35_발표자료_이보리-3](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/cb1f74a7-fa33-4519-8ddb-6938de2d5c48)

![item35_발표자료_이보리-4](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/df73dcf8-35f7-44a7-b1d4-d22c6caf20fb)

![item35_발표자료_이보리-5](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/0a92182e-6e00-41ff-86fb-9a864db6857a)

![item35_발표자료_이보리-6](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/8f2ce37f-7184-42a4-aa2c-fadece9cc9ba)

![item35_발표자료_이보리-7](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/42c5cc20-ed81-4328-a8aa-10c350f269e6)

![item35_발표자료_이보리-8](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/99f2957a-31be-4729-b649-3eeb38135d74)
