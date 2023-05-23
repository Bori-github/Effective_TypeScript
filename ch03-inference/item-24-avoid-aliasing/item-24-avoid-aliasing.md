# 일관성 있는 별칭 사용하기 | Effective TypeScript

## 새로운 별칭 사용하기

자바스크립트에서는 **어떤 값을 새로운 변수에 할당하여 사용**하기도 합니다.

![](https://hackmd-prod-images.s3-ap-northeast-1.amazonaws.com/uploads/upload_6b75c98b5dc769444a2501f8e9103b38.png?AWSAccessKeyId=AKIA3XSAAW6AWSKNINWO&Expires=1684842502&Signature=QMN2jInCTr28jfuXnzBXYGs7L4g%3D)

`boriAddress`라는 변수(별칭)를 선언하고 `bori.address`를 할당하였습니다.
`boriAddress`를 통해 `city`에 접근할 수 있고, `boriAddress`를 통해 `city`의 값을 변경하면 원본에서도 값이 변경됩니다.

이러한 **별칭을 남용하게 되면 제어 흐름을 분석하기 어려워집니다.**

## 별칭과 제어 흐름

![](https://hackmd-prod-images.s3-ap-northeast-1.amazonaws.com/uploads/upload_c08a41d2d0d3881d5844e1cc7b47c515.png?AWSAccessKeyId=AKIA3XSAAW6AWSKNINWO&Expires=1684842621&Signature=e1LsEaWLxb3UXvzl4y6kXjA6Jho%3D)

`Person` 이라는 인터페이스에 `address` 속성은 선택적 프로퍼티로 정의되어 있습니다.
`getAddress` 함수는 매개변수 `Person` 객체를 매개변수로 받고, 만약 `address` 속성이 존재한다면 `person.address.city`을 출력합니다.

`person.address`에 새로운 별칭을 할당하여 사용하면 어떻게 될까요?
(이때 `strictNullChecks`는 활성화된 상태입니다.)

![](https://hackmd-prod-images.s3-ap-northeast-1.amazonaws.com/uploads/upload_fe95ebbdedfe0924392bc6acf8adb537.png?AWSAccessKeyId=AKIA3XSAAW6AWSKNINWO&Expires=1684842675&Signature=S0jxdUCPwBIqgeJxaT3%2BkBBbSvg%3D)

`personAddress`는 `undefined` 일 수도 있다는 오류가 나타납니다.
그 이유는 `personAddress`라는 별칭이 제어 흐름 분석을 방해했기 때문입니다.

`person.address`의 타입은 속성 체크를 통해 정제되었지만, `personAddress`는 정제되지 않았기 때문에 오류가 발생했습니다.
이러한 오류는 **별칭을 일관성 있게 사용**하면 방지할 수 있습니다.

![](https://hackmd-prod-images.s3-ap-northeast-1.amazonaws.com/uploads/upload_fd0983c0650a3087efc17a7528a36d43.png?AWSAccessKeyId=AKIA3XSAAW6AWSKNINWO&Expires=1684842725&Signature=bPVL%2BSKFqFPVZrGR50cZxike%2FRg%3D)

속성 체크에 `personAddress`를 사용하면 타입 체커는 오류를 발생시키지 않습니다.

## 객체 비구조화 사용하기

여기에 한 가지 문제가 더 남아있습니다.
변수 `personAddress`는 `person.address`와 같은 값인데 단지 이름만 다르게 사용했다는 것입니다.
이를 간결하게 하기 위해 **객체 비구조화**를 이용할 수 있습니다.

![](https://hackmd-prod-images.s3-ap-northeast-1.amazonaws.com/uploads/upload_f949224962b7ef3406a398507793100f.png?AWSAccessKeyId=AKIA3XSAAW6AWSKNINWO&Expires=1684842741&Signature=NEeTSdSAh91NTEVaOhPp9sTf6V0%3D)

점(`.`) 표기법을 이용해 객체의 속성에 접근했던 코드가 비구조화를 통해 보다 간결해졌습니다.

객체 비구조화를 사용할 때 주의해야 할 부분이 있습니다.

![](https://hackmd-prod-images.s3-ap-northeast-1.amazonaws.com/uploads/upload_7b73fc7df669df08f1c1a69756a56a0e.png?AWSAccessKeyId=AKIA3XSAAW6AWSKNINWO&Expires=1684842777&Signature=Uss150HnlSCXzOTtjuYbkDvX6F8%3D)

위 예제에서 객체 비구조화를 사용하여 `address`라는 별칭을 사용하고, `address`가 `null이`나 `undefined`인 경우를 `if`문으로 분기처리 하였습니다. 이때 `if`문 내에서 `address`와 `bori.address`가 다른 타입을 나타내는 것을 볼 수 있습니다. 이것으로 두 값이 다른 값을 참조한다는 것을 알 수 있습니다.
따라서 객체 속성 체크에 사용할 때 주의해야 합니다.

> 이펙티브 타입스크립트 책의 예제에서는 `address`가 없는 경우 `if`문 내에서 어떤 함수의 호출로 인해 `bori.address`가 채워지면 `bori.address`와 `address`가 다른 값을 참조한다고 나와 있지만, 함수를 이용하지 않아도 각 타입을 확인해보면 타입이 다르다는 것을 알 수 있습니다.
> 그래서 저는 비구조화를 통해 사용한 별칭의 값을 기준으로 분기처리를 할 경우 어떤 함수를 호출하지 않아도 ***비구조화를 통해 사용한 별칭의 값*과 *원본 객체를 통해 접근한 속성의 값*이 다른 값을 참조**한다고 이해했습니다.

## 타입 정제 무효화

![](https://hackmd-prod-images.s3-ap-northeast-1.amazonaws.com/uploads/upload_c236907ccfdcd15aa5da9076e3953cd6.png?AWSAccessKeyId=AKIA3XSAAW6AWSKNINWO&Expires=1684842796&Signature=ugjoQqQJo8Uquix8ZeIrFVo3Qx0%3D)

분기처리를 통해 `bori.address`의 타입이 정제되었습니다. 하지만 `removeAddress` 함수 호출로 인해 `bori.address`가 제거될 가능성이 있습니다.
따라서 `bori.address`가 `undefined` 일 수도 있다는 것을 다시 명시하는 것이 안전하지만 함수를 호출할 때마다 속성 체크를 반복하는 것은 좋지 않습니다.

**타입스크립트는 함수가 타입 정제를 무효화하지 않는다고 가정하지만, 실제로는 무효화될 가능성이 있습니다.**

## 마무리

- 별칭을 남용한다면 제어 흐름을 분석하기 어려워집니다. 따라서 변수에 별칭을 사용할 때는 일관성있게 사용해야 합니다.
- 비구조화 문법을 사용해서 일관된 이름을 사용하는 것이 좋습니다.
- 함수 호출이 객체 속성의 타입 정제를 무효화 할 수 있다는 것을 주의해야 합니다.

