# React

## JSX란?

```JavaScript
const element = <h1>Hello, world!</h1>;
```
- 위에 희한한 태그 문법은 문자열도, HTML도 아니다. JSX라 하며 Javascript에 XML을 추가한 확장한 문법이다.
- JSX는 리액트로 프로젝트를 개발할 때 사용되므로 공식적인 자바스크립트 문법은 아니다.
- JSX는 HTML보다는 JavaScript에 가깝기 때문에, React DOM은 HTML 어트리뷰트 이름 대신 camelCase 프로퍼티 명명 규칙을 사용한다. 예를 들어, JSX에서 class는 className가 되고 tabindex는 tabIndex가 된다.
- 기본적으로 React DOM은 JSX에 삽입된 모든 값을 렌더링하기 전에 이스케이프 하므로 애플리케이션에서 명시적으로 작성되지 않은 내용은 주입되지 않는다. 모든 항목은 렌더링 되기 전에 문자열로 변환된다. 이런 특성으로 인해 XSS (cross-site-scripting) 공격을 방지할 수 있다.
    - 이스케이프: 특정 문자를 원래의 기능에서 벗어나게 변환하는 행위이다.
  
## 엘리먼트 렌더링
- React DOM은 해당 엘리먼트와 그 자식 엘리먼트를 이전의 엘리먼트와 비교하고 DOM을 원하는 상태로 만드는데 필요한 경우에만 DOM을 업데이트한다.
<img src="img/granular-dom-updates.gif" alt="granular-dom-updates.gif">


## state, props란?
- state 는 컴포넌트 내부에서 바꿀 수 있는, 바뀔 수 있는 값이다. 
  - 뷰에 렌더링돼야 하는 컴포넌트의 데이터를 저장하는 데 사용한다.
  - 상태는 데이터를 보유하고 시간이 지남에 따라 변경될 수 있다.
  - 이벤트 핸들러는 일반적으로 state를 업데이트한다.
- props는 부모 컴포넌트에서 설정하여 자식 컴포넌트로 전달하거나, 더 바깥의 컴포넌트에서 자기가 감싸고 있는 컴포넌트 내용을 표현하기 위해 사용한다.
  - 데이터, 이벤트 핸들러를 자식 컴포넌트에 전달하는 데 사용한다
  - props는 바뀔 수 없다. 한 번 설정되면 props를
    변경할 수 없다.
  - 상위 컴포넌트는 하위 컴포넌트에 대한 props를 설정한다.
## 이벤트 처리하기
React 엘리먼트에서 이벤트를 처리하는 방식은 DOM 엘리먼트에서 이벤트를 처리하는 방식과 매우 유사합니다. 몇 가지 문법 차이는 다음과 같다
- React의 이벤트는 소문자 대신 캐멀 케이스(camelCase)를 사용한다.
- JSX를 사용하여 문자열이 아닌 함수로 이벤트 핸들러를 전달한다.
```JavaScript
// 기존 HTML 코드
<button onclick="activateLasers()">
  Activate Lasers
</button>

// React 코드
<button onClick={activateLasers}>
  Activate Lasers
</button>

```

## 리스트와 Key
### 여러개의 컴포넌트 렌더링 하기
엘리먼트 모음을 만들고 중괄호 {}를 이용하여 JSX에 포함 시킬 수 있다.
```JavaScript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((numbers) =>
  {numbers}
);

const root = ReactDOM.createRoot(document.getElementById('root')); 
root.render({listItems});

<!-- result
1
2
3
4
5
-->
```
### Key
- 위에 코드를 실행하면 리스트의 각 항목에 key를 넣어야 한다는 경고가 표시된다. key는 엘리먼트 리스트를 만들 때 포함해야 하는 특수한 문자열 어트리뷰트이다.
- Key는 React가 어떤 항목을 변경, 추가 또는 삭제할지 식별하는 것을 돕는다.
- key는 엘리먼트에 안정적인 고유성을 부여하기 위해 배열 내부의 엘리먼트에 지정해야 한다.
- Key를 선택하는 가장 좋은 방법은 리스트의 다른 항목들 사이에서 해당 항목을 고유하게 식별할 수 있는 문자열을 사용하는 것이다. 대부분의 경우 데이터의 ID를 key로 사용한다.
- 최후의 수단으로 index를 key로 사용할 수 있다. 그러나 이방법은 성능이 저하되거나 컴포넌트의 state와 관련된 문제가 발생할 수 있다. 
  -   컴포넌트는 key 를 보고 갱신되고 재사용된다. index를 사용했다면 항목의 순서가 바뀌었을 경우 key 또한 바뀌었을 거고 이는 state를 엉망으로 만들거나 원하지 않는 방식으로 컴포넌트를 바꿀 수 있다. (https://ko.legacy.reactjs.org/docs/reconciliation.html#recursing-on-children)
- key는 형제 사이에서만 고유한 값이어야 한다.
  - Key는 배열 안에서 형제 사이에서 고유해야 하고 전체 범위에서 고유할 필요는 없다. 두 개의 다른 배열을 만들 때 동일한 key를 사용할 수 있다. (https://ko.legacy.reactjs.org/docs/lists-and-keys.html)
