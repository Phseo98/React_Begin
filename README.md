# React
React는 사용자 인터페이스 구축을 하기위해 효율적이고 유연한 js 라이브러리다. 

### 특징
1. Virtual DOM - Virtual Dom을 사용하여 변경된 부분만 DOM에 적용되 업데이트 되기 때문에 효율적임
2. component 기반 구조
3. 단방향 데이터 흐름 - 상위 컴포넌트에서 하위 컴포넌트로 한방향으로 흐리기 때문에 데이터 예측, 디버깅하기 효율적임
4. JSX문법
5. Single Page Application

### Virtual DOM 
컴포넌트가 렌더링 되면 DOM의 복제본을 메모리에 생성하고, 컴포넌트에 변경된 부분이 있으면 DOM과 복제본 DOM을 비교해 
변경된 부분만 DOM에 반영되어 렌더링 됨

#### 동작과정
1. 컴포넌트 랜더링 초기 가상DOM 생성
2. 컴포넌트 상태나 속성이 변경되면 새로운 가상DOM 생성
3. 초기 가상DOM이랑 새로운 가상DOM 비교
4. 변경된 부분만 실제 DOM에 적용

### JSX(JavascriptXML)
- js확장 문법으로 React에서 DOM element를 생성하기 위해 사용함
- JSX문법을 사용하면 브라우저가 이해할수 있도록 바벨을 이용해 js 코드 형태로 변환해야함
- js코드안에서 XML형식으로 작성되어 가독성을 높여줌

### component
- UI를 구성하는 독립적인 조각
- 함수형 컴포넌트, 클래스 컴포넌트로 작성될수 있음
- 첫글자는 대문자 why? 소문자로 하면 컴포넌트를 DOM태그로 처리하기 때문

### state
- 데이터 저장하는곳
- React 컴포넌트에서 관리되는 데이터의 현재상태를 나타냄
- 컴포넌트 상태 변경 시 React는 해당 컴포넌트를 리렌더링 하여 UI업데이트를 함
- useState훅을 사용하여 함수형 컴포넌트에서 state 관리 가능

### props
- 부모 컴포넌트로부터 자식 컴포넌트로 데이터를 전달하는데 사용함
- 읽기전용으로 전달되며 객체형태로 전달됨
``` JavaScript
// 부모 컴포넌트
function ParentComponent() {
  const message = "Hello from parent!";
  return <ChildComponent message={message} />;
}

// 자식 컴포넌트
function ChildComponent(props) {
  return <p>{props.message}</p>;
}

```
