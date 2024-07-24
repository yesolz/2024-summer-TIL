# JSX

## 개요

- 페이스북에서 개발했지만, 리액트에서만 사용하는 것은 아니다.
- JSX는 XML과 유사한 내장형 구문.
- 리액트에 종속적이지 않으며 독자적인 문법이다.
- JSX는 ECMAScript(자바스크립트 표준)의 일부가 아니다.
- 자바스크립트 엔진이나 브라우저에서 직접 실행되지 않는다.
- 반드시 트랜스파일러를 거쳐야 자바스크립트 런타임이 이해할 수 있는 코드로 변환된다.

## 목적

- HTML이나 XML을 자바스크립트 내부에 표현하는 것.
- 다양한 트랜스파일러에서 다양한 속성을 가진 트리 구조를 토큰화해 ECMAScript로 변환하는 데 초점.
- JSX 내부에 트리 구조로 표현하고 싶은 다양한 것들을 작성한 후, 이를 자바스크립트가 이해할 수 있는 코드로 변경하는 것이 목표.

## JSX의 정의

JSX는 네 가지 컴포넌트로 구성된다:

1. JSXElement
2. JSXAttributes
3. JSXChildren
4. JSXStrings

### JSXElement

- 가장 기본 요소로, HTML의 element와 비슷하다.
- JSXOpeningElement, JSXClosingElement, JSXSelfClosingElement, JSXFragment로 구성된다.
- 리액트에서는 사용자가 만든 컴포넌트는 반드시 대문자로 시작해야 한다.
- JSXElementName은 JSXElement의 요소 이름으로 쓸 수 있는 것. JSXIdentifier, JSXNamespacedName, JSXMemberExpression으로 구성된다.

### JSXAttributes

- JSXElement에 부여할 수 있는 속성을 의미한다.
- 단순히 속성을 의미하기 때문에 모든 경우에서 필수값이 아니고, 존재하지 않아도 에러가 나지 않는다.

### JSXChildren

- JSXElement의 자식 값.
- JSX는 속성을 가진 트릭 구조를 나타내기 위해 만들어졌기 때문에 JSX로 부모와 자식 관계를 나타낼 수 있다.

### JSXStrings

- JSX 내부의 문자열.
- JSXAttributeValue와 JSXText는 HTML과 JSX 사이에 복사와 붙여넣기를 쉽게 할 수 있도록 설계돼 있따.
- HTML에서 사용 가능한 문자열은 모두 JSXStrings에서도 가능하다.
- 따라서 자바스크립트와 한 가지 중요한 차이점이 발생하는데, \로 시작하는 이스케이프 문자 형태
- 자바스크립트에서 \는 특수문자 처리할 때 사용되지만, HTML에서는 아무런 제약 없이 사용할 수 있다. (현재의 JSX도 이스케이프 문자열로 처리하고 있지 않다.)

## JSX의 변환

- `@babel/plugin-transform-react-jsx`를 사용해 JSX 구문을 자바스크립트가 이해할 수 있는 형태로 변환한다.
- JSXElement를 첫 번째 인수로 선언해 요소를 정의하고, 이후 인수로 JSXChildren, JSXAttributes, JSXStrings를 넘겨준다.

### 변환 예시

```tsx
import { createElement, PropsWithChildren } from "react";

// 번거로운 삼항 연산자 사용
function TextOrHeading({
  isHeading,
  children,
}: PropsWithChildren<{ isHeading: boolean }>) {
  return isHeading ? (
    <h1 className="text">{children}</h1>
  ) : (
    <span className="text">{children}</span>
  );
}

// JSX 변환 특성을 활용한 간결한 처리
import { createElement } from "react";

function TextOrHeading({
  isHeading,
  children,
}: PropsWithChildren<{ isHeading: boolean }>) {
  return createElement(
    isHeading ? "h1" : "span",
    { className: "text" },
    children
  );
}
```

## 정리

- JSX 문법에는 있지만 리액트에서 사용하지 않는 요소도 있다: JSXNamespacedName, JSXMemberExpression.
- 다양한 라이브러리에서 JSX를 채용하고 있으며, 리액트와 다르게 특정 문법을 사용할 수도 있다.
- JSX는 자바스크립트 코드 내부에 HTML과 같은 트리 구조를 가진 컴포넌트를 표현할 수 있어 각광받고 있다.
- HTML과 자바스크립트 문법이 뒤섞여 코드 가독성을 해칠 수 있으며, 복잡성이 증가할 수 있으므로 주의가 필요하다.
- 리액트 애플리케이션을 만들 때, JSX가 어떻게 변환되고 어떤 결과물을 만드는지 이해하면 도움이 된다.
- 때에 따라서는 직접 createElement를 사용해 컴포넌트를 구성하는 것이 더 효율적일 수 있다.
