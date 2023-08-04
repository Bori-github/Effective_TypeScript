# DOM 계층 구조 이해하기 | Effective TypeScript

타입스크립트에서는 DOM 엘리먼트이 계층 구조를 파악하기 용이합니다.
Element와 EventTarget에 달려있는 Node의 구체적인 타입을 안다면 타입 오류를 디버깅할 수 있고, 언제 타입 단언을 사용해야 할지 알 수 있습니다.

## DOM 계층 구조

DOM 노드는 종류에 따라 각각 다른 프로퍼티를 지원합니다.

### `EventTarget`

- DOM 타입 중 가장 추상화된 타입입니다.
- 이벤트 리스너를 추가하거나 제거하고, 이벤트를 보내는 것을 할 수 있습니다.
- 루트에 있는 `EventTarget`이 모든 DOM 노드의 기초이기 때문에 DOM 노드에서 이벤트를 사용할 수 있습니다.

### `Node`

- DOM 노드의 베이스 역할을 합니다.
- `parentNode`, `nextSibling`, `childNodes` 등의 주요 트리 탐색 기능을 제공합니다.
- 텍스트 노드를 위한 `Text`, 요소 노드를 위한 `Element`, 주석 노드를 위한 `Comment`는 `Node` 타입을 상속받습니다.

만약 어떤 요소가 `children`과 `childNodes` 속성을 가지고 있다면,

- `children`은 자식 엘리먼트를 포함하는 배열과 유사한 구조인 `HTMLCollection` 입니다.
- `childNodes`은 배열과 유사한 구조인 `Node` 컬렉션인 `NodeList` 입니다.
  - `childNodes`은 엘리먼트 뿐만 아니라 텍스트와 주석도 포함됩니다.

예시를 통해 확인해봅니다.

![](https://hackmd.io/_uploads/SkZBf19i2.png)

> 위 예제는 [링크](https://ko.javascript.info/basic-dom-node-properties) 페이지의 일부이며, 임의로 `p` 태그에 `id` 속성을 지정하여 예제로 사용했습니다.

가장 바깥쪽의 엘리먼트는 `HTMLParagraphElement` 타입이고, `children`과 `childNodes` 속성을 가지고 있습니다.
이때 `children`은 자식으로 엘리먼트만 포함합니다.
반면 `childNodes`는 자식으로 엘리먼트와 텍스트도 포함합니다. 주석이 있다면 주석도 포함합니다.

### `Element`

- DOM 요소를 위한 베이스입니다.
- `nextElementSibling`, `children` 이나 `getElementsByTagName`, `querySelector` 같이 요소 전용 탐색을 도와주는 프로퍼티나 메서드가 `Element`를 기반으로 합니다.
- 브라우저는 HTML뿐만 아니라 XML, SVG도 지원하는데 `Element`는 이와 관련된 `SVGElement`, `XMLElement`, `HTMLElement` 의 베이스 역할을 합니다.

### `HTMLElement`

- HTML 요소 노드의 베이스 역할을 합니다.
- `HTMLxxxElement는` 실제 HTML 요소에 대응하고 `HTMLElement`를 상속받습니다.
  - 예시로 `HTMLInputElement`는 `<input>` 요소에 대응합니다.

### `HTMLxxxElement`

- `HTMLxxxElement` 형태의 특정 엘리먼트들은 자신만의 고유한 속성을 가지고 있습니다.
- `HTMLImageElement`에는 `src` 속성이 있고, `HTMLInputElement`에는 `value` 속성이 있습니다.
- 이런 속성에 접근하려면, 타입 정보가 실제 엘리먼트 타입이어야 하기 때문에 구체적으로 타입을 지정해야 합니다.

보통 HTML 태그 값에 해당하는 리터럴 값을 사용하면 DOM에 대한 정확한 타입을 얻을 수 있습니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/ec114c87-8c71-4036-9233-1bbf12c3d6f4)

하지만 요소의 정보를 알 수 없는 경우 정확한 타입을 얻을 수 없습니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/3cb0be8f-9b6e-4cb3-ac0d-d1b0fd62a724)

일반적으로 타입 단언문을 지양해야 하지만, DOM 관련해서는 타입스크립트보다 개발자가 더 정확히 알고 있습니다. 따라서 다음과 같이 단언문을 사용할 수 있습니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/93892b46-4cb6-45c8-a609-68170d146357)

만약 strictNullChecks가 설정되어 있다면, `document.getElementById`가 null인 경우도 체크해야 합니다. 그리고 그에 따른 분기처리가 필요합니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/f2b201fd-1172-45a8-933a-ecb00281abbf)

DOM 타입의 계층 구조를 이미지로 나타내면 다음과 같습니다.

![image](https://github.com/Bori-github/Effective_TypeScript/assets/85009583/04e6d706-91cf-4d91-b3c7-7250c9dc8d3c)

## `Event` 타입 계층 구조

DOM 계층 구조 뿐만 아니라 `Event` 타입에도 변도의 계층 구조가 있습니다. 또한 각 타입마다 고유의 속성을 가지고 있습니다.

### `Event`

- 가장 추상화된 이벤트로 모든 이벤트에 공통된 속성과 메서드를 가집니다.
- DOM 요소는 이벤트를 받고("수신"), 받은 이벤트를 "처리"할 수 있습니다.

#### `UIEvent`

- 모든 종류의 사용자 인터페이스 이벤트를 나타냅니다.
- `MouseEvent`, `TouchEvent`, `WheelEvent`, `KeyboardEvent`는 `UIEvent`를 상속받습니다.

#### `MouseEvent`

- 사용자가 마우스와 같은 포인팅 장치를 사용해 상호작용할 때 발생하는 이벤트를 나타냅니다.

#### `TouchEvent`

- 모바일 기기와 같이 터치를 감지할 수 있는 표면과 접촉 상태가 변경될 때 발생하는 이벤트를 나타냅니다.

#### `WheelEvent`

- 사용자가 마우스 휠이나 그와 비슷한 장치를 움직여 발생하는 이벤트를 나타냅니다.

#### `KeyboardEvent`

- 사용자가 키보드의 키를 눌렀을 때 발생하는 이벤트를 나타냅니다.

예시를 통해 조금 더 이해를 해봅시다.

```typescript
// Event 타입 지정
function handleDrag(e: Event) {
  const dragStart = [e.clientX, e.clientY];
  // 'Event' 형식에 'clientX' 속성이 없습니다.
  // 'Event' 형식에 'clientY' 속성이 없습니다.
}
```

위의 예제에서 이벤트의 타입에 `Event`를 지정하면 해당 속성이 없다는 에러메시지가 나타납니다.
고유의 속성을 사용하기 위해 이벤트를 구체적으로 지정해야 합니다.

```typescript
// MouseEvent 타입 지정
function handleDrag(e: MouseEvent) {
  const dragStart = [e.clientX, e.clientY];
  // OK
}
```

구체적인 `MouseEvent` 타입을 적용하여 에러 없이 `clientX`, `clientY` 속성을 사용할 수 있습니다.

## 마무리

- DOM에는 타입 계층 구조가 있고, 타입스크립트에서 DOM 타입은 중요한 정보입니다.
- DOM 계층 구조의 각 타입간의 차이점과 이벤트 타입의 차이점을 알아야 고유의 속성을 에러없이 사용할 수 있습니다.
- DOM 엘리먼트와 이벤트에는 구체적인 타입 정보를 사용하거나, 타입스크립트가 추론할 수 있도록 문맥 정보를 활용해야 합니다.

> #### 참고
>
> - [주요 노드 프로퍼티](https://ko.javascript.info/basic-dom-node-properties)
> - [Event - MDN](https://developer.mozilla.org/ko/docs/Web/API/Event)
