# 일관성 있는 별칭 사용하기 | Effective TypeScript

## 새로운 별칭 사용하기

자바스크립트에서는 **어떤 값을 새로운 변수에 할당하여 사용**하기도 합니다.

![img1](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/3127ebdb-f327-4ad2-ad09-912a6c3515de)

`boriAddress`라는 변수(별칭)를 선언하고 `bori.address`를 할당하였습니다.
`boriAddress`를 통해 `city`에 접근할 수 있고, `boriAddress`를 통해 `city`의 값을 변경하면 원본에서도 값이 변경됩니다.

이러한 **별칭을 남용하게 되면 제어 흐름을 분석하기 어려워집니다.**

## 별칭과 제어 흐름

![img2](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/7f09b9f7-9425-4182-8169-b7b944e9807c)

`Person` 이라는 인터페이스에 `address` 속성은 선택적 프로퍼티로 정의되어 있습니다.
`getAddress` 함수는 매개변수 `Person` 객체를 매개변수로 받고, 만약 `address` 속성이 존재한다면 `person.address.city`을 출력합니다.

`person.address`에 새로운 별칭을 할당하여 사용하면 어떻게 될까요?
(이때 `strictNullChecks`는 활성화된 상태입니다.)

![Group 143](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/1a1c67fc-899b-471b-bfc2-68015f1b7228)

`personAddress`는 `undefined` 일 수도 있다는 오류가 나타납니다.
그 이유는 `personAddress`라는 별칭이 제어 흐름 분석을 방해했기 때문입니다.

`person.address`의 타입은 속성 체크를 통해 정제되었지만, `personAddress`는 정제되지 않았기 때문에 오류가 발생했습니다.
이러한 오류는 **별칭을 일관성 있게 사용**하면 방지할 수 있습니다.

![img10](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/9bd937b8-c5f8-4f8f-8d9e-dcf7d12d266f)

속성 체크에 `personAddress`를 사용하면 타입 체커는 오류를 발생시키지 않습니다.

## 객체 비구조화 사용하기

여기에 한 가지 문제가 더 남아있습니다.
변수 `personAddress`는 `person.address`와 같은 값인데 단지 이름만 다르게 사용했다는 것입니다.
이를 간결하게 하기 위해 **객체 비구조화**를 이용할 수 있습니다.

![img7](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/ce6f6ac7-9439-4b91-9498-92ebb9ccbe06)

비구조화 문법을 사용하여 일관된 이름을 사용할 수 있고 또한, 점(`.`) 표기법을 이용해 객체의 속성에 접근했던 코드를 보다 간결하게 작성할 수 있습니다.

객체 비구조화를 사용할 때 주의해야 할 부분이 있습니다.

![Group 145](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/0fe0c400-8e53-4043-b3fb-ba7fd29cfc79)

위 예제에서 객체 비구조화를 사용하여 `address` 변수를 사용하고, `address`가 `null`이나 `undefined`인 경우를 `if`문으로 분기처리 하였습니다. 이때 `if`문 내에서 `address`와 `bori.address`가 다른 타입을 나타내는 것을 볼 수 있습니다. 이것으로 두 값이 다른 값을 참조한다는 것을 알 수 있습니다.
따라서 비구조화 문법을 사용하여 객체 속성 체크할 때 주의해야 합니다.

> 이펙티브 타입스크립트 책의 예제에서는 `address`가 없는 경우 `if`문 내에서 어떤 함수의 호출로 인해 `bori.address`가 채워지면 `bori.address`와 `address`가 다른 값을 참조한다고 나와 있지만, 함수를 이용하지 않아도 각 타입을 확인해보면 타입이 다르다는 것을 알 수 있습니다.
> 그래서 저는 비구조화의 변수를 기준으로 분기처리를 할 경우 어떤 함수를 호출하지 않아도 ***비구조화를 사용한 변수의 값*과 *원본 객체를 통해 접근한 속성의 값*이 다른 값을 참조**한다고 이해했습니다.

## 타입 정제 무효화

![Group 146](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/78bff155-7b1c-413c-86ca-cb4c6357bfc0)

분기처리를 통해 `bori.address`의 타입이 정제되었습니다. 하지만 `removeAddress` 함수 호출로 인해 `bori.address`가 제거될 가능성이 있습니다.
따라서 `bori.address`가 `undefined` 일 수도 있다는 것을 다시 명시하는 것이 안전하지만 함수를 호출할 때마다 속성 체크를 반복하는 것은 좋지 않습니다.

**타입스크립트는 함수가 타입 정제를 무효화하지 않는다고 가정하지만, 실제로는 무효화될 가능성이 있습니다.**

속성보다 지역 변수를 사용하면 타입 정제 무효화 가능성을 낮출 수 있습니다.
타입스크립트의 제어 흐름 분석은 지역 변수를 사용할 경우 잘 동작하고, 지역 변수는 함수 내부에서 선언되어 사용되기 때문에 변수의 타입을 정확하게 추론할 수 있습니다.
예제에서 `bori.address`를 사용한는 것보다 비구조화 문법을 사용하여 `address`를 지역 변수로 뽑아내어 사용하면 `address`의 타입은 정확히 유지됩니다. 다만 비구조화 문법 사용의 주의사항처럼 `bori.address`와 `address`의 값이 같지 않을 수 있습니다.

## 마무리
- 별칭을 남용한다면 제어 흐름을 분석하기 어려워집니다. 따라서 변수에 별칭을 사용할 때는 일관성있게 사용해야 합니다.
- 비구조화 문법을 사용해서 일관된 이름을 사용하는 것이 좋습니다.
- 함수 호출로 인해 객체 속성의 타입 정제를 무효화할 수 있으므로, 속성보다 비구조화하여 뽑아낸 지역 변수를 사용하면 타입 정제를 믿을 수 있습니다.
- 이 때 객체 비구조화하여 뽑아낸 변수와 원본 객체를 통해 접근한 속성의 값이 다를 수 있음을 주의해야합니다.
