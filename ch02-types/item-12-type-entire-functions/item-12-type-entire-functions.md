# 함수 표현식에 타입 적용하기 | Effective TypeScript

## 타입스크립트에서 함수 정의하기

함수를 정의하는 방법은 크게 두 가지로 나눌 수 있습니다.
- 함수 선언문
	```typescript
	function funcStatement(params: number): number { /* ... */ };
	```
- 함수 표현식
	```typescript
	const funcExpression1 = function(params: number): number { /* ... */ };
	const funcExpression2 = (params: number): number => { /* ... */ };
	```

타입스크립트에서는 함수 표현식을 사용하는 것이 좋습니다.
**함수의 매개변수부터 반환값까지 전체를 함수 타입으로 선언**하여 함수 표현식에 **재사용**할 수 있기 때문입니다.

![](https://i.imgur.com/s73wvo9.png)

위의 예제 코드에서 **선언된 함수 타입을 함수 표현식에서는 재사용**할 수 있고, 에디터에서 `params`에 마우스를 올려 보면, `params`의 타입을 `number`로 인식하고 있다는 것을 알 수 있습니다.
하지만 **함수 선언문에는 함수 타입 재사용을 할 수 없습니다.**

## 함수 타입 선언

함수 타입은 재사용 할 수 있습니다. 따라서, 함수 타입의 선언은 **불필요한 코드의 반복을 줄입니다.**

다음은 함수 선언문으로 정의된 사칙연산을 수행하는 함수입니다.
각 함수의 매개변수 타입을 각각 정의하고 있습니다.
![](https://i.imgur.com/fiYDafB.png)

반복되는 함수 시그니처를 하나의 함수 타입으로 통합할 수 있습니다.
따라서 다음과 같이 적용하게 되면 매개변수의 타입과 반환 타입의 **반복된 코드를 줄일 수 있고**, **함수 구현부도 분리**되어 로직이 보다 분명해집니다.

![](https://i.imgur.com/0wOToxe.png)

## 다른 함수 시그니처 참조

다음은 웹브라우저에서 `fetch` 함수가 특정 리소스에 HTTP 요청을 보내는 예제입니다.
그리고 `response.json()` 사용해 응답 데이터를 추출합니다.

![](https://i.imgur.com/Elo7mcq.png)

만약 정상적으로 응답했다면 JSON 형태의 데이터를 받지만, 그렇지 않은 경우 응답은 JSON 형식이 아닌 오류 메시지를 담은 `rejected` 프로미스가 반환됩니다.

상태 체크를 수행할 함수에 `fetch`의 타입을 적용하여 다음과 같이 코드를 작성할 수 있습니다.
다른 함수의 시그니처를 참조하려면 `typeof fn`을 사용합니다.

![](https://i.imgur.com/hlSqkOO.png)

- 함수 표현식으로 작성
- 함수 전체에 타입(`typeof fetch`) 적용

이를 통해, 타입스크립트가 `input`과 `init`의 **타입을 추론**할 수 있게 하고 `checkedFetch`의 **반환 타입을 보장**합니다.

만약 `throw` 대신 `return`을 사용한다면, 타입스크립트는 오류를 잡아냅니다.

![](https://i.imgur.com/GZZZyL2.png)

함수 표현식 전체 타입을 정의하는 것은 코드를 간결하게 할 뿐만 아니라 **안전하게 합니다.**

## 마무리
타입스크립트에서 함수 정의는 함수 표현식을 사용하는 것이 좋습니다.
함수를 작성할 때 매개변수의 타입과 반환 타입을 반복해서 작성하지 않고 함수 전체의 타입을 선언하여 적용해야 합니다.
이를 통해 불필요한 코드를 줄이고 보다 안전하게 함수를 사용할 수 있습니다.