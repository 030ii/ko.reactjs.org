---
id: hooks-faq
title: Hook 자주 묻는 질문
permalink: docs/hooks-faq.html
prev: hooks-reference.html
---

*Hook*은 React 16.8에 새로 추가되었습니다. Class를 작성하지 않고 state 및 기타 React 기능을 사용할 수 있습니다.

이 페이지는 [Hook](/docs/hooks-overview.html) 자주 묻는 질문에 대한 답변입니다.

<!--
  if you ever need to regenerate this, this snippet in the devtools console might help:

  $$('.anchor').map(a =>
    `${' '.repeat(2 * +a.parentNode.nodeName.slice(1))}` +
    `[${a.parentNode.textContent}](${a.getAttribute('href')})`
  ).join('\n')
-->

* **[적용 전략](#adoption-strategy)**
  * [어떤 버전의 React가 Hook을 포함합니까?](#which-versions-of-react-include-hooks)
  * [모든 class 컴포넌트를 다시 작성해야 합니까?](#do-i-need-to-rewrite-all-my-class-components)
  * [Class로 하지 못하는 것 중에 Hook으로 가능한 것이 무엇인가요?](#what-can-i-do-with-hooks-that-i-couldnt-with-classes)
  * [React 지식은 얼마나 관련이 있습니까?](#how-much-of-my-react-knowledge-stays-relevant)
  * [Hook이나 class 또는 두 가지를 모두 사용해야 합니까?](#should-i-use-hooks-classes-or-a-mix-of-both)
  * [Hook이 class의 모든 사용 사례를 커버합니까?](#do-hooks-cover-all-use-cases-for-classes)
  * [Hook이 render props 및 고차 컴포넌트를 대체합니까?](#do-hooks-replace-render-props-and-higher-order-components)
  * [Redux connect()와 React Router와 같은 인기 있는 API에 대해 Hook은 무엇을 의미합니까?](#what-do-hooks-mean-for-popular-apis-like-redux-connect-and-react-router)
  * [Hook은 정적 타이핑과 함께 작동합니까?](#do-hooks-work-with-static-typing)
  * [Hook을 사용하는 컴포넌트 테스트하는 방법?](#how-to-test-components-that-use-hooks)
  * [Lint 규칙은 정확히 무엇을 시행합니까?](#what-exactly-do-the-lint-rules-enforce)
* **[Class에서 Hook으로](#from-classes-to-hooks)**
  * [생명주기 메서드가 Hook에 어떻게 대응합니까?](#how-do-lifecycle-methods-correspond-to-hooks)
  * [Hook을 사용하여 데이터 가져오기를 수행하려면 어떻게 해야 합니까?](#how-can-i-do-data-fetching-with-hooks)
  * [인스턴스 변수와 같은 것이 있습니까?](#is-there-something-like-instance-variables)
  * [하나 또는 여러 state 변수를 사용해야 합니까?](#should-i-use-one-or-many-state-variables)
  * [업데이트에만 effect를 실행할 수 있습니까?](#can-i-run-an-effect-only-on-updates)
  * [이전 props 또는 state를 얻는 방법?](#how-to-get-the-previous-props-or-state)
  * [함수 안에 오래된 props나 state가 보이는 이유는 무엇입니까?](#why-am-i-seeing-stale-props-or-state-inside-my-function)
  * [getDerivedStateFromProps를 어떻게 구현합니까?](#how-do-i-implement-getderivedstatefromprops)
  * [forceUpdate와 같은 것이 있습니까?](#is-there-something-like-forceupdate)
  * [함수 컴포넌트에 ref를 만들 수 있습니까?](#can-i-make-a-ref-to-a-function-component)
  * [DOM 노드를 측정하려면 어떻게 해야 합니까?](#how-can-i-measure-a-dom-node)
  * [const [thing, setThing] = useState()는 무엇을 의미합니까?](#what-does-const-thing-setthing--usestate-mean)
* **[성능 최적화](#performance-optimizations)**
  * [업데이트 시 effect를 건너뛸 수 있습니까?](#can-i-skip-an-effect-on-updates)
  * [의존성 목록에서 함수를 생략하는 것이 안전합니까?](#is-it-safe-to-omit-functions-from-the-list-of-dependencies)
  * [effect 의존성이 너무 자주 변경되면 어떻게 해야 합니까?](#what-can-i-do-if-my-effect-dependencies-change-too-often)
  * [shouldComponentUpdate는 어떻게 구현합니까?](#how-do-i-implement-shouldcomponentupdate)
  * [계산을 메모이제이션 하는 법?](#how-to-memoize-calculations)
  * [고비용의 객체를 지연해서 생성하는 법?](#how-to-create-expensive-objects-lazily)
  * [렌더링에서 함수를 만들기 때문에 Hook이 느려집니까?](#are-hooks-slow-because-of-creating-functions-in-render)
  * [콜백 전달을 피하는 법?](#how-to-avoid-passing-callbacks-down)
  * [useCallback에서 자주 변경되는 값을 읽는 방법?](#how-to-read-an-often-changing-value-from-usecallback)
* **[Hook의 이면](#under-the-hood)**
  * [React는 Hook 호출을 컴포넌트와 어떻게 연관시키는가?](#how-does-react-associate-hook-calls-with-components)
  * [Hook에 대한 선행 기술은 무엇입니까?](#what-is-the-prior-art-for-hooks)

## 적용 전략 {#adoption-strategy}

### 어떤 버전의 React가 Hook을 포함합니까? {#which-versions-of-react-include-hooks}

16.8.0부터 React에는 React Hook의 안정적인 구현이 포함됩니다.

* React DOM
* React Native
* React DOM Server
* React 테스트 렌더러
* React 얕은 렌더러

**Hook을 사용하려면 모든 React 패키지가 16.8.0 이상이어야합니다**. 업데이트하는 것을 (예: React DOM) 잊어버리면 Hook이 작동하지 않습니다.

[React Native 0.59](https://reactnative.dev/blog/2019/03/12/releasing-react-native-059) and above support Hooks.

### 모든 class 컴포넌트를 다시 작성해야 합니까? {#do-i-need-to-rewrite-all-my-class-components}

아닙니다. React에서 class를 삭제할 [계획은 없습니다](/docs/hooks-intro.html#gradual-adoption-strategy). 우리는 제품을 출시할 때마다 재작성을 할 여유가 없습니다. 새 코드에서 Hook을 사용하는 것이 좋습니다.

### Class로 하지 못하는 것 중에 Hook으로 가능한 것이 무엇인가요? {#what-can-i-do-with-hooks-that-i-couldnt-with-classes}

Hook은 컴포넌트 간에 기능을 재사용할 수 있는 강력하고 표현적인 새로운 방법을 제공합니다. ["자신만의 Hook 만들기"](/docs/hooks-custom.html)는 가능한 것을 엿볼 수 있게 해줍니다. React 핵심 팀 구성원이 작성한 [이 기사](https://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889)에서는 Hook이 제공할 새로운 기능에 대해 자세히 설명합니다.

### React 지식은 얼마나 관련이 있습니까? {#how-much-of-my-react-knowledge-stays-relevant}

Hook은 state, 생명주기, context 및 ref와 같은 이미 알고 있는 React 기능을 사용하는 보다 직접적인 방법입니다. React가 어떻게 작동하는지 근본적으로 바꿀 수 없으며 컴포넌트, props 및 하향식 데이터 흐름에 대한 지식도 마찬가지로 중요합니다.

Hook에는 독자적인 학습 곡선이 있습니다. 이 문서에 누락된 것이 있으면 [문제를 제기](https://github.com/reactjs/reactjs.org/issues/new)하면 도움을 제공해 드리겠습니다.

### Hook이나 class 또는 두 가지를 모두 사용해야 합니까? {#should-i-use-hooks-classes-or-a-mix-of-both}

준비가 되면 작성하는 새 컴포넌트에서 Hook을 시도해 보는 것이 좋습니다. 팀의 모든 구성원이 사용하고 이 문서에 익숙해 지도록 하십시오. 일부러 다시 작성하지 않는 이상 (예: 버그 수정) 기존 class를 Hook으로 고쳐 쓰는 것은 추천하지 않습니다.

Class 컴포넌트 *내부에서* Hook을 사용할 수는 없지만, class와 함수 컴포넌트를 단일 트리에서 Hook과 섞어서 사용할 수 있습니다. 컴포넌트가 class인지 Hook을 사용하는 함수인지 여부는 해당 컴포넌트의 구현 세부 사항입니다. 장기적으로 우리는 Hook이 사람들이 React 컴포넌트를 작성하는 주요 방법이 될 것으로 기대합니다.

### Hook이 class의 모든 사용 사례를 커버합니까? {#do-hooks-cover-all-use-cases-for-classes}

우리의 목표는 Hook이 class의 모든 사용 사례를 가능한 한 빨리 커버하게 하는 것입니다. 드문 `getSnapshotBeforeUpdate`, `getDerivedStateFromError` 및 `componentDidCatch` 생명주기에 해당하는 Hook은 아직 없지만, 곧 추가할 계획입니다.

Hook의 초기 단계이며 일부 타사 라이브러리는 현재 Hook과 호환되지 않을 수 있습니다.

### Hook이 render props 및 고차 컴포넌트를 대체합니까? {#do-hooks-replace-render-props-and-higher-order-components}

종종 render props와 고차 컴포넌트는 하나의 자식만 렌더링합니다. 우리는 Hook이 이 사용 사례를 처리하는 더 간단한 방법이라고 생각합니다. 여전히 두 패턴 모두를 쓸 수 있습니다. (예를 들어, 가상 스크롤러 컴포넌트에는 `renderItem` props가 있거나 시각적 컨테이너 컴포넌트에는 자체 DOM 구조가 있을 수 있습니다) 그러나 대부분의 경우 Hook은 충분하며 코드 트리의 중첩을 줄이는 데 도움이 될 수 있습니다.

### Redux `connect()`와 React Router와 같은 인기 있는 API에 대해 Hook은 무엇을 의미합니까? {#what-do-hooks-mean-for-popular-apis-like-redux-connect-and-react-router}

여태껏 쓰던 API를 계속 사용할 수 있습니다; 앞으로도 계속 작동할 것 입니다.

v7.1.0부터 React Redux는 [Hook API를 지원하고](https://react-redux.js.org/api/hooks) `useDispatch` 또는 `useSelector`와 같은 Hook을 노출합니다.

v5.1 이후 React Router는 [Hook을 지원합니다](https://reacttraining.com/react-router/web/api/Hooks).

다른 라이브러리도 나중에 Hook을 지원할 수 있습니다.

### Hook은 정적 타이핑과 함께 작동합니까? {#do-hooks-work-with-static-typing}

Hook은 정적 타이핑을 염두에 두고 설계되었습니다. 함수이기 때문에 고차 컴포넌트와 같은 패턴보다 타입을 명시하기가 더 쉽습니다. 최신 Flow 및 TypeScript React 정의에는 React Hook 지원이 포함됩니다.

중요한 점은, 커스텀 Hook은 더 엄격하게 타이핑하려는 경우 React API를 제한할 수 있는 기능을 제공합니다. React는 기초 요소를 제공하지만, 기본 제공 방식과 다른 방식으로 조합 할 수 있습니다.

### Hook을 사용하는 컴포넌트 테스트하는 방법? {#how-to-test-components-that-use-hooks}

React의 관점에서 Hook을 사용하는 컴포넌트는 일반적인 컴포넌트입니다. 테스트 솔루션이 React internals에 의존하지 않는 경우 Hook이 있는 컴포넌트 테스트는 일반적으로 컴포넌트를 테스트하는 방법과 다르지 않아야 합니다.

>주의
>
>[테스팅 방안](/docs/testing-recipes.html)에는 복사하여 붙여넣을 수 있는 많은 예제가 포함되어 있습니다.

예를 들어 여기 이 계수기 컴포넌트가 있다고 가정해 보겠습니다:

```js
function Example() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

React DOM을 사용하여 테스트하겠습니다. 브라우저에서 발생하는 상황과 동작이 일치하도록 코드 렌더링을 포장하고 이를 [`ReactTestUtils.act()`](/docs/test-utils.html#act) 호출로 업데이트합니다.

```js{3,20-22,29-31}
import React from 'react';
import ReactDOM from 'react-dom';
import { act } from 'react-dom/test-utils';
import Counter from './Counter';

let container;

beforeEach(() => {
  container = document.createElement('div');
  document.body.appendChild(container);
});

afterEach(() => {
  document.body.removeChild(container);
  container = null;
});

it('can render and update a counter', () => {
  // Test first render and effect
  act(() => {
    ReactDOM.render(<Counter />, container);
  });
  const button = container.querySelector('button');
  const label = container.querySelector('p');
  expect(label.textContent).toBe('You clicked 0 times');
  expect(document.title).toBe('You clicked 0 times');

  // Test second render and effect
  act(() => {
    button.dispatchEvent(new MouseEvent('click', {bubbles: true}));
  });
  expect(label.textContent).toBe('You clicked 1 times');
  expect(document.title).toBe('You clicked 1 times');
});
```

`act()` 호출은 그 안의 효과를 플러시합니다.

커스텀 Hook을 테스트해야 하는 경우 테스트에서 컴포넌트를 작성하고 Hook을 사용하여 이를 수행 할 수 있습니다. 그런 다음 작성한 컴포넌트를 테스트 할 수 있습니다.

상용구를 줄이려면 [React Testing Library](https://testing-library.com/react)를 사용하는 것이 좋습니다. 이 라이브러리는 최종 사용자와 마찬가지로 컴포넌트를 사용하는 테스트 작성을 장려하도록 설계되었습니다.

자세한 내용은 [테스팅 방안](/docs/testing-recipes.html)을 확인하십시오.

### [Lint 규칙](https://www.npmjs.com/package/eslint-plugin-react-hooks)은 정확히 무엇을 시행합니까? {#what-exactly-do-the-lint-rules-enforce}

버그를 피하고자 [Hook 규칙](/docs/hooks-rules.html)을 시행하는 [ESLint 플러그인](https://www.npmjs.com/package/eslint-plugin-react-hooks)을 제공합니다. "`use`"로 시작하는 모든 함수와 Hook 바로 뒤에 대문자가 있다고 가정합니다. 우리는 이 휴리스틱이 완벽하지 않고 오 탐지가 있을 수 있다는 점을 인식하지만, 생태계 전반의 협약이 없으면 훅을 제대로 작동시킬 수 있는 방법이 없습니다 -- 더 긴 이름은 사람들이 Hook을 채택하거나 협약을 따르지 못하게 합니다.

특히, 규칙은 이것들을 시행합니다.

* Hook에 대한 호출은 `PascalCase` 함수 (컴포넌트로 가정) 또는 다른 `useSomething` 함수 (커스텀 Hook으로 가정) 내에 있습니다.
* 모든 렌더링에서 Hook은 동일한 순서로 호출됩니다.

휴리스틱이 몇 가지 더 있으며, 추후 오 탐지를 피해 버그를 찾기 위해 규칙을 미세 조정함에 따라 변경될 수 있습니다.

## Class에서 Hook으로 {#from-classes-to-hooks}

### 생명주기 메서드가 Hook에 어떻게 대응합니까? {#how-do-lifecycle-methods-correspond-to-hooks}

* `constructor`: 함수 컴포넌트는 constructor가 필요하지 않습니다. [`useState`](/docs/hooks-reference.html#usestate) 호출에서 state를 초기화 할 수 있습니다. 초기 state를 계산하는 것이 비싸면 `useState`에 함수를 전달할 수 있습니다.

* `getDerivedStateFromProps`: [대신 렌더링](#how-do-i-implement-getderivedstatefromprops)하는 동안 업데이트 예약.

* `shouldComponentUpdate`: [아래의](#how-do-i-implement-shouldcomponentupdate) `React.memo`를 참조하십시오.

* `render`: 이것은 함수 컴포넌트 본체 자체입니다.

* `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`: [`useEffect` Hook](/docs/hooks-reference.html#useeffect)은 이들의 모든 조합을 표현할 수 있습니다. ([흔하거나](#can-i-run-an-effect-only-on-updates) [그렇지 않은](#can-i-skip-an-effect-on-updates) 경우 포함).

* `getSnapshotBeforeUpdate`, `componentDidCatch` 그리고 `getDerivedStateFromError`: 이러한 메서드에 대한 Hook은 없지만, 곧 추가될 예정입니다.

### Hook을 사용하여 데이터 가져오기를 수행하려면 어떻게 해야 합니까? {#how-can-i-do-data-fetching-with-hooks}

다음은 시작하기 위한 [짧은 데모](https://codesandbox.io/s/jvvkoo8pq3)입니다. 자세한 내용은 Hook을 사용한 데이터 가져오기를 다룬 [이 기사](https://www.robinwieruch.de/react-hooks-fetch-data/)를 확인하십시오.

### 인스턴스 변수와 같은 것이 있습니까? {#is-there-something-like-instance-variables}

네! [`useRef()`](/docs/hooks-reference.html#useref) Hook은 DOM ref만을 위한 것이 아닙니다. "ref" 객체는 `현재` 프로퍼티가 변경할 수 있고 어떤 값이든 보유할 수 있는 일반 컨테이너입니다. 이는 class의 인스턴스 프로퍼티와 유사합니다.

`useEffect` 내부에서 쓸 수 있습니다.

```js{2,8}
function Timer() {
  const intervalRef = useRef();

  useEffect(() => {
    const id = setInterval(() => {
      // ...
    });
    intervalRef.current = id;
    return () => {
      clearInterval(intervalRef.current);
    };
  });

  // ...
}
```

인터벌을 설정하고 싶다면 ref가 필요하지 않지만 (`id`는 로컬 effect일 수 있습니다), 이벤트 핸들러에서 인터벌을 지우고 싶을 때 유용합니다.

```js{3}
  // ...
  function handleCancelClick() {
    clearInterval(intervalRef.current);
  }
  // ...
```

개념적으로, class의 인스턴스 변수와 ref를 비슷하게 생각할 수 있습니다. [지연 초기화](#how-to-create-expensive-objects-lazily)를 수행하지 않는 한, 렌더링 중에 ref 설정을 피하십시오 -- 이것은 놀라운 상황을 초래할 수 있습니다. 대신, 일반적으로 이벤트 핸들러와 effect에서 ref를 수정하는 것이 좋습니다.

### 하나 또는 여러 state 변수를 사용해야 합니까? {#should-i-use-one-or-many-state-variables}

Class를 배운 후라면, `useState ()`를 한 번만 호출하고 모든 state를 단일 객체에 넣고 싶을 수 있습니다. 원하시면 그렇게 할 수 있습니다. 다음은 마우스 움직임을 따르는 컴포넌트의 예입니다. 포인터의 위치와 크기를 로컬 state에 유지합니다.

```js
function Box() {
  const [state, setState] = useState({ left: 0, top: 0, width: 100, height: 100 });
  // ...
}
```

이제 사용자가 마우스를 움직일 때 `left`과 `top`의 포지션을 변경하는 로직을 작성하고 싶다고 가정해 보겠습니다. 이러한 필드를 이전 state 개체에 수동으로 병합하는 방법에 유의하십시오.

```js{4,5}
  // ...
  useEffect(() => {
    function handleWindowMouseMove(e) {
      // Spreading "...state" ensures we don't "lose" width and height
      setState(state => ({ ...state, left: e.pageX, top: e.pageY }));
    }
    // Note: this implementation is a bit simplified
    window.addEventListener('mousemove', handleWindowMouseMove);
    return () => window.removeEventListener('mousemove', handleWindowMouseMove);
  }, []);
  // ...
```

이는 state 변수를 업데이트할 때 그 값을 *대체*하기 때문입니다. 이것은 업데이트된 필드를 객체에 *병합*하는 class의 `this.setState`와 다릅니다.

자동 병합을 놓친 경우 개체 state 업데이트를 병합하는 커스텀 `useLegacyState` Hook을 작성할 수 있습니다. 그러나, **함께변경 되는 값에 따라 state를 여러 state 변수로 분할하는 것을 추천합니다.**

예를 들어 컴포넌트 상태를 `position` 및 `size` 객체로 분할하고 병합할 필요 없이 항상 `position`을 대체 할 수 있습니다.

```js{2,7}
function Box() {
  const [position, setPosition] = useState({ left: 0, top: 0 });
  const [size, setSize] = useState({ width: 100, height: 100 });

  useEffect(() => {
    function handleWindowMouseMove(e) {
      setPosition({ left: e.pageX, top: e.pageY });
    }
    // ...
```

독립된 state 변수를 분리하면 또 다른 이점이 있습니다. 예를 들어 나중에 관련 로직을 커스텀 Hook으로 쉽게 추출 할 수 있습니다.

```js{2,7}
function Box() {
  const position = useWindowPosition();
  const [size, setSize] = useState({ width: 100, height: 100 });
  // ...
}

function useWindowPosition() {
  const [position, setPosition] = useState({ left: 0, top: 0 });
  useEffect(() => {
    // ...
  }, []);
  return position;
}
```

코드를 변경하지 않고 `position` state 변수에 대한 `useState` 호출과 관련 effect를 커스텀 Hook으로 옮길 수 있었던 방법에 유의하십시오. 모든 state가 단일 객체에 있으면 추출하기가 더 어려울 것입니다.

모든 state를 단일 `useState` 호출에 넣고 필드마다 `useState` 호출을 두는 방법도 쓸 수 있습니다. 컴포넌트는 이러한 두 극단 사이의 균형을 찾고 관련 state를 몇 개의 독립 state 변수로 그룹화할 때 가장 읽기 쉬운 경향이 있습니다. State 로직이 복잡해지면 [reducer로 관리](/docs/hooks-reference.html#usereducer), 또는 커스텀 Hook을 사용하는 것이 좋습니다.

### 업데이트에만 effect를 실행할 수 있습니까? {#can-i-run-an-effect-only-on-updates}

이것은 드문 사용 사례입니다. 필요한 경우 [변경 가능한 ref를 사용하여](#is-there-something-like-instance-variables) 첫 번째 또는 후속 렌더링에 있는지에 해당하는 부울 값을 수동으로 저장한 다음, 해당 플래그를 확인할 수 있습니다. (이 작업을 자주 수행하는 경우 커스텀 Hook을 만들 수 있습니다.)

### 이전 props 또는 state를 얻는 방법? {#how-to-get-the-previous-props-or-state}

Currently, you can do it manually [with a ref](#is-there-something-like-instance-variables).

```js{6,8}
function Counter() {
  const [count, setCount] = useState(0);

  const prevCountRef = useRef();
  useEffect(() => {
    prevCountRef.current = count;
  });
  const prevCount = prevCountRef.current;

  return <h1>Now: {count}, before: {prevCount}</h1>;
}
```

This might be a bit convoluted but you can extract it into a custom Hook.

```js{3,7}
function Counter() {
  const [count, setCount] = useState(0);
  const prevCount = usePrevious(count);
  return <h1>Now: {count}, before: {prevCount}</h1>;
}

function usePrevious(value) {
  const ref = useRef();
  useEffect(() => {
    ref.current = value;
  });
  return ref.current;
}
```

Note how this would work for props, state, or any other calculated value.

```js{5}
function Counter() {
  const [count, setCount] = useState(0);

  const calculation = count + 100;
  const prevCalculation = usePrevious(calculation);
  // ...
```

It's possible that in the future React will provide a `usePrevious` Hook out of the box since it's a relatively common use case.

See also [the recommended pattern for derived state](#how-do-i-implement-getderivedstatefromprops).

### 함수 안에 오래된 props나 state가 보이는 이유는 무엇입니까? {#why-am-i-seeing-stale-props-or-state-inside-my-function}

Any function inside a component, including event handlers and effects, "sees" the props and state from the render it was created in. For example, consider code like this.

```js
function Example() {
  const [count, setCount] = useState(0);

  function handleAlertClick() {
    setTimeout(() => {
      alert('You clicked on: ' + count);
    }, 3000);
  }

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
      <button onClick={handleAlertClick}>
        Show alert
      </button>
    </div>
  );
}
```

If you first click "Show alert" and then increment the counter, the alert will show the `count` variable **at the time you clicked the "Show alert" button**. This prevents bugs caused by the code assuming props and state don't change.

If you intentionally want to read the *latest* state from some asynchronous callback, you could keep it in [a ref](/docs/hooks-faq.html#is-there-something-like-instance-variables), mutate it, and read from it.

Finally, another possible reason you're seeing stale props or state is if you use the "dependency array" optimization but didn't correctly specify all the dependencies. For example, if an effect specifies `[]` as the second argument but reads `someProp` inside, it will keep "seeing" the initial value of `someProp`. The solution is to either remove the dependency array, or to fix it. Here's [how you can deal with functions](#is-it-safe-to-omit-functions-from-the-list-of-dependencies), and here's [other common strategies](#what-can-i-do-if-my-effect-dependencies-change-too-often) to run effects less often without incorrectly skipping dependencies.

>Note
>
>We provide an [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) ESLint rule as a part of the [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation) package. It warns when dependencies are specified incorrectly and suggests a fix.

### `getDerivedStateFromProps`를 어떻게 구현합니까? {#how-do-i-implement-getderivedstatefromprops}

While you probably [don't need it](/blog/2018/06/07/you-probably-dont-need-derived-state.html), in rare cases that you do (such as implementing a `<Transition>` component), you can update the state right during rendering. React will re-run the component with updated state immediately after exiting the first render so it wouldn't be expensive.

Here, we store the previous value of the `row` prop in a state variable so that we can compare.

```js
function ScrollView({row}) {
  const [isScrollingDown, setIsScrollingDown] = useState(false);
  const [prevRow, setPrevRow] = useState(null);

  if (row !== prevRow) {
    // Row changed since last render. Update isScrollingDown.
    setIsScrollingDown(prevRow !== null && row > prevRow);
    setPrevRow(row);
  }

  return `Scrolling down: ${isScrollingDown}`;
}
```

This might look strange at first, but an update during rendering is exactly what `getDerivedStateFromProps` has always been like conceptually.

### forceUpdate와 같은 것이 있습니까? {#is-there-something-like-forceupdate}

Both `useState` and `useReducer` Hooks [bail out of updates](/docs/hooks-reference.html#bailing-out-of-a-state-update) if the next value is the same as the previous one. Mutating state in place and calling `setState` will not cause a re-render.

Normally, you shouldn't mutate local state in React. However, as an escape hatch, you can use an incrementing counter to force a re-render even if the state has not changed.

```js
  const [ignored, forceUpdate] = useReducer(x => x + 1, 0);

  function handleClick() {
    forceUpdate();
  }
```

Try to avoid this pattern if possible.

### 함수 컴포넌트에 ref를 만들 수 있습니까? {#can-i-make-a-ref-to-a-function-component}

While you shouldn't need this often, you may expose some imperative methods to a parent component with the [`useImperativeHandle`](/docs/hooks-reference.html#useimperativehandle) Hook.

### DOM 노드를 측정하려면 어떻게 해야 합니까? {#how-can-i-measure-a-dom-node}

One rudimentary way to measure the position or size of a DOM node is to use a [callback ref](/docs/refs-and-the-dom.html#callback-refs). React will call that callback whenever the ref gets attached to a different node. Here is a [small demo](https://codesandbox.io/s/l7m0v5x4v9):

```js{4-8,12}
function MeasureExample() {
  const [height, setHeight] = useState(0);

  const measuredRef = useCallback(node => {
    if (node !== null) {
      setHeight(node.getBoundingClientRect().height);
    }
  }, []);

  return (
    <>
      <h1 ref={measuredRef}>Hello, world</h1>
      <h2>The above header is {Math.round(height)}px tall</h2>
    </>
  );
}
```

We didn't choose `useRef` in this example because an object ref doesn't notify us about *changes* to the current ref value. Using a callback ref ensures that [even if a child component displays the measured node later](https://codesandbox.io/s/818zzk8m78) (e.g. in response to a click), we still get notified about it in the parent component and can update the measurements.

Note that we pass `[]` as a dependency array to `useCallback`. This ensures that our ref callback doesn't change between the re-renders, and so React won't call it unnecessarily.

In this example, the callback ref will be called only when the component mounts and unmounts, since the rendered `<h1>` component stays present throughout any rerenders. If you want to be notified any time a component resizes, you may want to use [`ResizeObserver`](https://developer.mozilla.org/en-US/docs/Web/API/ResizeObserver) or a third-party Hook built on it.

If you want, you can [extract this logic](https://codesandbox.io/s/m5o42082xy) into a reusable Hook:

```js{2}
function MeasureExample() {
  const [rect, ref] = useClientRect();
  return (
    <>
      <h1 ref={ref}>Hello, world</h1>
      {rect !== null &&
        <h2>The above header is {Math.round(rect.height)}px tall</h2>
      }
    </>
  );
}

function useClientRect() {
  const [rect, setRect] = useState(null);
  const ref = useCallback(node => {
    if (node !== null) {
      setRect(node.getBoundingClientRect());
    }
  }, []);
  return [rect, ref];
}
```


### `const [thing, setThing] = useState()`는 무엇을 의미합니까? {#what-does-const-thing-setthing--usestate-mean}

If you're not familiar with this syntax, check out the [explanation](/docs/hooks-state.html#tip-what-do-square-brackets-mean) in the State Hook documentation.


## 성능 최적화 {#performance-optimizations}

### 업데이트 시 effect를 건너뛸 수 있습니까? {#can-i-skip-an-effect-on-updates}

Yes. See [conditionally firing an effect](/docs/hooks-reference.html#conditionally-firing-an-effect). Note that forgetting to handle updates often [introduces bugs](/docs/hooks-effect.html#explanation-why-effects-run-on-each-update), which is why this isn't the default behavior.

### 의존성 목록에서 함수를 생략하는 것이 안전합니까? {#is-it-safe-to-omit-functions-from-the-list-of-dependencies}

Generally speaking, no.

```js{3,8}
function Example({ someProp }) {
  function doSomething() {
    console.log(someProp);
  }

  useEffect(() => {
    doSomething();
  }, []); // 🔴 This is not safe (it calls `doSomething` which uses `someProp`)
}
```

It's difficult to remember which props or state are used by functions outside of the effect. This is why **usually you'll want to declare functions needed by an effect *inside* of it.** Then it's easy to see what values from the component scope that effect depends on.

```js{4,8}
function Example({ someProp }) {
  useEffect(() => {
    function doSomething() {
      console.log(someProp);
    }

    doSomething();
  }, [someProp]); // ✅ OK (our effect only uses `someProp`)
}
```

If after that we still don't use any values from the component scope, it's safe to specify `[]`.

```js{7}
useEffect(() => {
  function doSomething() {
    console.log('hello');
  }

  doSomething();
}, []); // ✅ OK in this example because we don't use *any* values from component scope
```

Depending on your use case, there are a few more options described below.

>Note
>
>We provide the [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) ESLint rule as a part of the [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation) package. It helps you find components that don't handle updates consistently.

Let's see why this matters.

If you specify a [list of dependencies](/docs/hooks-reference.html#conditionally-firing-an-effect) as the last argument to `useEffect`, `useLayoutEffect`, `useMemo`, `useCallback`, or `useImperativeHandle`, it must include all values that are used inside the callback and participate in the React data flow. That includes props, state, and anything derived from them.

It is **only** safe to omit a function from the dependency list if nothing in it (or the functions called by it) references props, state, or values derived from them. This example has a bug.

```js{5,12}
function ProductPage({ productId }) {
  const [product, setProduct] = useState(null);

  async function fetchProduct() {
    const response = await fetch('http://myapi/product/' + productId); // Uses productId prop
    const json = await response.json();
    setProduct(json);
  }

  useEffect(() => {
    fetchProduct();
  }, []); // 🔴 Invalid because `fetchProduct` uses `productId`
  // ...
}
```

**The recommended fix is to move that function _inside_ of your effect**. That makes it easy to see which props or state your effect uses, and to ensure they're all declared.

```js{5-10,13}
function ProductPage({ productId }) {
  const [product, setProduct] = useState(null);

  useEffect(() => {
    // By moving this function inside the effect, we can clearly see the values it uses.
    async function fetchProduct() {
      const response = await fetch('http://myapi/product/' + productId);
      const json = await response.json();
      setProduct(json);
    }

    fetchProduct();
  }, [productId]); // ✅ Valid because our effect only uses productId
  // ...
}
```

This also allows you to handle out-of-order responses with a local variable inside the effect.

```js{2,6,10}
  useEffect(() => {
    let ignore = false;
    async function fetchProduct() {
      const response = await fetch('http://myapi/product/' + productId);
      const json = await response.json();
      if (!ignore) setProduct(json);
    }

    fetchProduct();
    return () => { ignore = true };
  }, [productId]);
```

We moved the function inside the effect so it doesn't need to be in its dependency list.

>Tip
>
>Check out [this small demo](https://codesandbox.io/s/jvvkoo8pq3) and [this article](https://www.robinwieruch.de/react-hooks-fetch-data/) to learn more about data fetching with Hooks.

**If for some reason you _can't_ move a function inside an effect, there are a few more options.**

* **You can try moving that function outside of your component**. In that case, the function is guaranteed to not reference any props or state, and also doesn't need to be in the list of dependencies.
* If the function you're calling is a pure computation and is safe to call while rendering, you may **call it outside of the effect instead,** and make the effect depend on the returned value.
* As a last resort, you can **add a function to effect dependencies but _wrap its definition_** into the [`useCallback`](/docs/hooks-reference.html#usecallback) Hook. This ensures it doesn't change on every render unless *its own* dependencies also change.

```js{2-5}
function ProductPage({ productId }) {
  // ✅ Wrap with useCallback to avoid change on every render
  const fetchProduct = useCallback(() => {
    // ... Does something with productId ...
  }, [productId]); // ✅ All useCallback dependencies are specified

  return <ProductDetails fetchProduct={fetchProduct} />;
}

function ProductDetails({ fetchProduct }) {
  useEffect(() => {
    fetchProduct();
  }, [fetchProduct]); // ✅ All useEffect dependencies are specified
  // ...
}
```

Note that in the above example we **need** to keep the function in the dependencies list. This ensures that a change in the `productId` prop of `ProductPage` automatically triggers a refetch in the `ProductDetails` component.

### effect 의존성이 너무 자주 변경되면 어떻게 해야 합니까? {#what-can-i-do-if-my-effect-dependencies-change-too-often}

Sometimes, your effect may be using state that changes too often. You might be tempted to omit that state from a list of dependencies, but that usually leads to bugs.

```js{6,9}
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const id = setInterval(() => {
      setCount(count + 1); // This effect depends on the `count` state
    }, 1000);
    return () => clearInterval(id);
  }, []); // 🔴 Bug: `count` is not specified as a dependency

  return <h1>{count}</h1>;
}
```

The empty set of dependencies, `[]`, means that the effect will only run once when the component mounts, and not on every re-render. The problem is that inside the `setInterval` callback, the value of `count` does not change, because we've created a closure with the value of `count` set to `0` as it was when the effect callback ran. Every second, this callback then calls `setCount(0 + 1)`, so the count never goes above 1.

Specifying `[count]` as a list of dependencies would fix the bug, but would cause the interval to be reset on every change. Effectively, each `setInterval` would get one chance to execute before being cleared (similar to a `setTimeout`.) That may not be desirable. To fix this, we can use the [functional update form of `setState`](/docs/hooks-reference.html#functional-updates). It lets us specify *how* the state needs to change without referencing the *current* state:

```js{6,9}
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const id = setInterval(() => {
      setCount(c => c + 1); // ✅ This doesn't depend on `count` variable outside
    }, 1000);
    return () => clearInterval(id);
  }, []); // ✅ Our effect doesn't use any variables in the component scope

  return <h1>{count}</h1>;
}
```

(The identity of the `setCount` function is guaranteed to be stable so it's safe to omit.)

Now, the `setInterval` callback executes once a second, but each time the inner call to `setCount` can use an up-to-date value for `count` (called `c` in the callback here.)

In more complex cases (such as if one state depends on another state), try moving the state update logic outside the effect with the [`useReducer` Hook](/docs/hooks-reference.html#usereducer). [This article](https://adamrackis.dev/state-and-use-reducer/) offers an example of how you can do this. **The identity of the `dispatch` function from `useReducer` is always stable** — even if the reducer function is declared inside the component and reads its props.

As a last resort, if you want something like `this` in a class, you can [use a ref](/docs/hooks-faq.html#is-there-something-like-instance-variables) to hold a mutable variable. Then you can write and read to it. For example.

```js{2-6,10-11,16}
function Example(props) {
  // Keep latest props in a ref.
  const latestProps = useRef(props);
  useEffect(() => {
    latestProps.current = props;
  });

  useEffect(() => {
    function tick() {
      // Read latest props at any time
      console.log(latestProps.current);
    }

    const id = setInterval(tick, 1000);
    return () => clearInterval(id);
  }, []); // This effect never re-runs
}
```

Only do this if you couldn't find a better alternative, as relying on mutation makes components less predictable. If there's a specific pattern that doesn't translate well, [file an issue](https://github.com/facebook/react/issues/new) with a runnable example code and we can try to help.

### `shouldComponentUpdate`는 어떻게 구현합니까? {#how-do-i-implement-shouldcomponentupdate}

You can wrap a function component with `React.memo` to shallowly compare its props.

```js
const Button = React.memo((props) => {
  // your component
});
```

It's not a Hook because it doesn't compose like Hooks do. `React.memo` is equivalent to `PureComponent`, but it only compares props. (You can also add a second argument to specify a custom comparison function that takes the old and new props. If it returns true, the update is skipped.)

`React.memo` doesn't compare state because there is no single state object to compare. But you can make children pure too, or even [optimize individual children with `useMemo`](/docs/hooks-faq.html#how-to-memoize-calculations).

### 계산을 메모이제이션 하는 법? {#how-to-memoize-calculations}

The [`useMemo`](/docs/hooks-reference.html#usememo) Hook lets you cache calculations between multiple renders by "remembering" the previous computation.

```js
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

This code calls `computeExpensiveValue(a, b)`. But if the dependencies `[a, b]` haven't changed since the last value, `useMemo` skips calling it a second time and simply reuses the last value it returned.

Remember that the function passed to `useMemo` runs during rendering. Don't do anything there that you wouldn't normally do while rendering. For example, side effects belong in `useEffect`, not `useMemo`.

**You may rely on `useMemo` as a performance optimization, not as a semantic guarantee.** In the future, React may choose to "forget" some previously memoized values and recalculate them on next render, e.g. to free memory for offscreen components. Write your code so that it still works without `useMemo` — and then add it to optimize performance. (For rare cases when a value must *never* be recomputed, you can [lazily initialize](#how-to-create-expensive-objects-lazily) a ref.)

Conveniently, `useMemo` also lets you skip an expensive re-render of a child.

```js
function Parent({ a, b }) {
  // Only re-rendered if `a` changes:
  const child1 = useMemo(() => <Child1 a={a} />, [a]);
  // Only re-rendered if `b` changes:
  const child2 = useMemo(() => <Child2 b={b} />, [b]);
  return (
    <>
      {child1}
      {child2}
    </>
  )
}
```

Note that this approach won't work in a loop because Hook calls [can't](/docs/hooks-rules.html) be placed inside loops. But you can extract a separate component for the list item, and call `useMemo` there.

### 고비용의 객체를 지연해서 생성하는 법? {#how-to-create-expensive-objects-lazily}

`useMemo` lets you [memoize an expensive calculation](#how-to-memoize-calculations) if the dependencies are the same. However, it only serves as a hint, and doesn't *guarantee* the computation won't re-run. But sometimes you need to be sure an object is only created once.

**The first common use case is when creating the initial state is expensive.**

```js
function Table(props) {
  // ⚠️ createRows() is called on every render
  const [rows, setRows] = useState(createRows(props.count));
  // ...
}
```

To avoid re-creating the ignored initial state, we can pass a **function** to `useState`.

```js
function Table(props) {
  // ✅ createRows() is only called once
  const [rows, setRows] = useState(() => createRows(props.count));
  // ...
}
```

React will only call this function during the first render. See the [`useState` API reference](/docs/hooks-reference.html#usestate).

**You might also occasionally want to avoid re-creating the `useRef()` initial value.** For example, maybe you want to ensure some imperative class instance only gets created once.

```js
function Image(props) {
  // ⚠️ IntersectionObserver is created on every render
  const ref = useRef(new IntersectionObserver(onIntersect));
  // ...
}
```

`useRef` **does not** accept a special function overload like `useState`. Instead, you can write your own function that creates and sets it lazily.

```js
function Image(props) {
  const ref = useRef(null);

  // ✅ IntersectionObserver is created lazily once
  function getObserver() {
    if (ref.current === null) {
      ref.current = new IntersectionObserver(onIntersect);
    }
    return ref.current;
  }

  // When you need it, call getObserver()
  // ...
}
```

This avoids creating an expensive object until it's truly needed for the first time. If you use Flow or TypeScript, you can also give `getObserver()` a non-nullable type for convenience.


### 렌더링에서 함수를 만들기 때문에 Hook이 느려집니까? {#are-hooks-slow-because-of-creating-functions-in-render}

No. In modern browsers, the raw performance of closures compared to classes doesn't differ significantly except in extreme scenarios.

In addition, consider that the design of Hooks is more efficient in a couple ways.

* Hooks avoid a lot of the overhead that classes require, like the cost of creating class instances and binding event handlers in the constructor.

* **Idiomatic code using Hooks doesn't need the deep component tree nesting** that is prevalent in codebases that use higher-order components, render props, and context. With smaller component trees, React has less work to do.

Traditionally, performance concerns around inline functions in React have been related to how passing new callbacks on each render breaks `shouldComponentUpdate` optimizations in child components. Hooks approach this problem from three sides.

* The [`useCallback`](/docs/hooks-reference.html#usecallback) Hook lets you keep the same callback reference between re-renders so that `shouldComponentUpdate` continues to work.

    ```js{2}
    // Will not change unless `a` or `b` changes
    const memoizedCallback = useCallback(() => {
      doSomething(a, b);
    }, [a, b]);
    ```

* The [`useMemo`](/docs/hooks-faq.html#how-to-memoize-calculations) Hook makes it easier to control when individual children update, reducing the need for pure components.

* Finally, the [`useReducer`](/docs/hooks-reference.html#usereducer) Hook reduces the need to pass callbacks deeply, as explained below.

### 콜백 전달을 피하는 법? {#how-to-avoid-passing-callbacks-down}

We've found that most people don't enjoy manually passing callbacks through every level of a component tree. Even though it is more explicit, it can feel like a lot of "plumbing".

In large component trees, an alternative we recommend is to pass down a `dispatch` function from [`useReducer`](/docs/hooks-reference.html#usereducer) via context.

```js{4,5}
const TodosDispatch = React.createContext(null);

function TodosApp() {
  // Note: `dispatch` won't change between re-renders
  const [todos, dispatch] = useReducer(todosReducer);

  return (
    <TodosDispatch.Provider value={dispatch}>
      <DeepTree todos={todos} />
    </TodosDispatch.Provider>
  );
}
```

Any child in the tree inside `TodosApp` can use the `dispatch` function to pass actions up to `TodosApp`.

```js{2,3}
function DeepChild(props) {
  // If we want to perform an action, we can get dispatch from context.
  const dispatch = useContext(TodosDispatch);

  function handleClick() {
    dispatch({ type: 'add', text: 'hello' });
  }

  return (
    <button onClick={handleClick}>Add todo</button>
  );
}
```

This is both more convenient from the maintenance perspective (no need to keep forwarding callbacks), and avoids the callback problem altogether. Passing `dispatch` down like this is the recommended pattern for deep updates.

Note that you can still choose whether to pass the application *state* down as props (more explicit) or as context (more convenient for very deep updates). If you use context to pass down the state too, use two different context types -- the `dispatch` context never changes, so components that read it don't need to rerender unless they also need the application state.

### `useCallback`에서 자주 변경되는 값을 읽는 방법? {#how-to-read-an-often-changing-value-from-usecallback}

>Note
>
>We recommend to [pass `dispatch` down in context](#how-to-avoid-passing-callbacks-down) rather than individual callbacks in props. The approach below is only mentioned here for completeness and as an escape hatch.
>
>Also note that this pattern might cause problems in the [concurrent mode](/blog/2018/03/27/update-on-async-rendering.html). We plan to provide more ergonomic alternatives in the future, but the safest solution right now is to always invalidate the callback if some value it depends on changes.

In some rare cases you might need to memoize a callback with [`useCallback`](/docs/hooks-reference.html#usecallback) but the memoization doesn't work very well because the inner function has to be re-created too often. If the function you're memoizing is an event handler and isn't used during rendering, you can use [ref as an instance variable](#is-there-something-like-instance-variables), and save the last committed value into it manually.

```js{6,10}
function Form() {
  const [text, updateText] = useState('');
  const textRef = useRef();

  useEffect(() => {
    textRef.current = text; // Write it to the ref
  });

  const handleSubmit = useCallback(() => {
    const currentText = textRef.current; // Read it from the ref
    alert(currentText);
  }, [textRef]); // Don't recreate handleSubmit like [text] would do

  return (
    <>
      <input value={text} onChange={e => updateText(e.target.value)} />
      <ExpensiveTree onSubmit={handleSubmit} />
    </>
  );
}
```

This is a rather convoluted pattern but it shows that you can do this escape hatch optimization if you need it. It's more bearable if you extract it to a custom Hook.

```js{4,16}
function Form() {
  const [text, updateText] = useState('');
  // Will be memoized even if `text` changes:
  const handleSubmit = useEventCallback(() => {
    alert(text);
  }, [text]);

  return (
    <>
      <input value={text} onChange={e => updateText(e.target.value)} />
      <ExpensiveTree onSubmit={handleSubmit} />
    </>
  );
}

function useEventCallback(fn, dependencies) {
  const ref = useRef(() => {
    throw new Error('Cannot call an event handler while rendering.');
  });

  useEffect(() => {
    ref.current = fn;
  }, [fn, ...dependencies]);

  return useCallback(() => {
    const fn = ref.current;
    return fn();
  }, [ref]);
}
```

In either case, we **don't recommend this pattern** and only show it here for completeness. Instead, it is preferable to [avoid passing callbacks deep down](#how-to-avoid-passing-callbacks-down).


## Hook의 이면 {#under-the-hood}

### React는 Hook 호출을 컴포넌트와 어떻게 연관시키는가? {#how-does-react-associate-hook-calls-with-components}

React keeps track of the currently rendering component. Thanks to the [Rules of Hooks](/docs/hooks-rules.html), we know that Hooks are only called from React components (or custom Hooks -- which are also only called from React components).

There is an internal list of "memory cells" associated with each component. They're just JavaScript objects where we can put some data. When you call a Hook like `useState()`, it reads the current cell (or initializes it during the first render), and then moves the pointer to the next one. This is how multiple `useState()` calls each get independent local state.

### Hook에 대한 선행 기술은 무엇입니까? {#what-is-the-prior-art-for-hooks}

Hooks synthesize ideas from several different sources.

* Our old experiments with functional APIs in the [react-future](https://github.com/reactjs/react-future/tree/master/07%20-%20Returning%20State) repository.
* React community's experiments with render prop APIs, including [Ryan Florence](https://github.com/ryanflorence)'s [Reactions Component](https://github.com/reactions/component).
* [Dominic Gannaway](https://github.com/trueadm)'s [`adopt` keyword](https://gist.github.com/trueadm/17beb64288e30192f3aa29cad0218067) proposal as a sugar syntax for render props.
* State variables and state cells in [DisplayScript](http://displayscript.org/introduction.html).
* [Reducer components](https://reasonml.github.io/reason-react/docs/en/state-actions-reducer.html) in ReasonReact.
* [Subscriptions](http://reactivex.io/rxjs/class/es6/Subscription.js~Subscription.html) in Rx.
* [Algebraic effects](https://github.com/ocamllabs/ocaml-effects-tutorial#2-effectful-computations-in-a-pure-setting) in Multicore OCaml.

[Sebastian Markbåge](https://github.com/sebmarkbage) came up with the original design for Hooks, later refined by [Andrew Clark](https://github.com/acdlite), [Sophie Alpert](https://github.com/sophiebits), [Dominic Gannaway](https://github.com/trueadm), and other members of the React team.
