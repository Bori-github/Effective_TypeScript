# 몽키 패치보다는 안전한 타입을 사용하기 | Effective TypeScript

## 몽키 패치란?
몽키 패치란 런타임 중인 프로그램의 내용이 변경되는 것을 의미합니다.
JavaScript는 객체와 클래스에 임의의 속성을 추가할 수 있을 만큼 유연합니다. 따라서, 객체의 메소드를 선언시점이 아닌 사용시점에 변경해서 사용할 수 있습니다.

#### 몽키 패치 예시 코드 및 결과

- `console.log` 메소드 변경하여 사용하기
  ```javascript
  console.log_changed = console.log;
  console.log = (arguments) => {console.log_changed(`몽키 패치 테스트 : ${arguments}`)};

  console.log('테스트 완료');
  ```

- 결과

  ![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/d5000bf6-9274-4812-bf51-d7c66c756a0d)

또한 다음과 같이 사용할 수도 있습니다.

#### `window`나 `document`에 값을 할당하여 전역 변수 만들기

```javascript
document.monkey_patch = 'Tada!'
```

#### DOM 요소에 데이터를 추가하기

```javascript
const el = document.getElementById('monkey_patch');
el.result = 'Tada!'
```

#### 내장 기능의 프로토타입에 속성 추가하기

```javascript
> RegExp.prototype.monkey_patch = 'Tada!';
'Tada!'
> /123/.monkey_patch
'Tada!'
```

그런데 문제점이 있습니다.
예시 중 `RegExp.prototype.monkey_patch = 'Tada!';`를 적용했는데 임의로 작성한 정규식(`/123/`)에도 `monkey_patch` 속성이 추가되어 값을 가지고 있습니다.

또 다른 문제점 `window` 나 DOM 노드에 데이터를 추가할 경우 해당 데이터는 전역 변수가 된다는 점입니다. 전역 변수를 사용하면 문제점이 발생하는데 그에 대한 사이드 이펙트를 고려해야 합니다.

> 일반적인 프로그래밍에서 몽키 패치는 안티 패턴이지만, 좋은 사례도 있습니다.
> 좋은 사례 중 하나는 Babel 입니다.
> Babel 모던 자바스크립트에서 구형 브라우저들을 지원하기 위한 트랜스파일러로 Polyfill 기능을 지원합니다.
> Polyfill은 구형 브라우저들을 위해 모던 자바스크립트의 기능을 최대한 사용할 수 있게 몽키패칭해줍니다.

## 몽키 패치에 타입스크립트 더하기

몽키 패치에 타입스크립트 더하면 어떻게 될까요?

`document` 객체에 속성을 추가하여 전역 변수를 만들어 사용해봅시다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/cc56438c-0969-49dd-928b-89ef8ea51b1f)


### 문제점

이 때 타입 체커는 `Document`의 내장 속성에 대해 알고 있지만, 임의로 추가한 속성에 대해서는 알지 못해 다음과 같은 에러가 발생합니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/c4f1bf63-53e2-4670-b8a1-f10f875c6c3f)

이 문제점은 `any` 단언문을 통해 간단히 해결할 수 있습니다.
하지만 `any`의 사용으로 타입의 안정성이 낮아지고, 오타가 발생해도 타입 체커가 오류를 발생시키지 않습니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/78792925-5b6f-4ea7-a3fc-efcd659e8971)

가장 좋은 방법은 `document` 또는 DOM으로부터 데이터를 분리하는 것이지만 그럴 수 없는 경우가 존재합니다.

## 몽키 패치보다는 안전한 타입을 사용하기

위의 문제점을 다음과 같은 방법으로 해결해봅시다.

### `interface`의 보강(augmentation) 사용하기

`interface`의 보강 기능을 사용하여 문제를 해결할 수 있습니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/721c0208-aad2-424d-816b-1860ea700734)

보강을 사용했을 경우 다음과 같은 장점이 있습니다.
- 타입 체커가 오타나 잘못된 타입의 할당을 오류로 표시하여 **타입의 안정성**을 높일 수 있습니다.
- 속성에 **주석**을 붙일 수 있습니다.
- 속성에 **자동완성**을 사용할 수 있습니다.
- 몽키 패치가 어떤 부분에 적용되었는지 **정확한 기록**이 남습니다.

> 타입스크립트 파일을 ES Module을 이용해 사용할 경우 global 선언을 추가해야 합니다.
>
> ![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/75e47243-3c50-45ec-8aba-887ca7dac010)

보강을 사용할 때 주의해야할 점이 있습니다.
보강은 **전역적**으로 적용되기 때문에, 코드의 다른 부분이나 라이브러리로부터 분리할 수 없습니다.
그리고 애플리케이션이 실행되는 동안 속성을 할당하면 **실행 시점에서 보강을 적용할 수 없습니다.**

### 더 구체적인 타입 단언문 사용하기

`Document` 타입을 확장하여 타입 단언을 적용할 수 있습니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/9bc33e96-9759-43a9-b303-ff13b9e948c9)

이 방법은 `Document` 타입을 건드리지 않고 새로운 타입을 생성했기 때문에 전역적으로 적용되는 문제를 해결하여 `import` 하는 곳에서만 사용할 수 있습니다.

## 마무리
- 몽키 패치를 남용하지 않도록 구조를 설계하는 것이 좋습니다.
- 내장 타입에 데이터를 저장해야 하는 경우, 보강 기능을 이용하거나 내장 타입을 확장하여 타입 단언을 적용하는 방법과 같은 안전한 타입 접근법을 사용해야 합니다.
- 보강 기능을 사용할 경우 모듈의 영역 문제를 이해하고 사용해야 합니다.

> #### 참고
> - [What is Monkey patch?](https://juunone.netlify.app/development/monkey-patch/)