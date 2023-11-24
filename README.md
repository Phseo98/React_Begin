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

#### useState
useState는 React에서 컴포넌트가 변경되면 자동으로 리랜더링 해주는 방법

``` javascript
// 2개의 인덱스로 가진 배열로 반환
// [0] data, [1] 0번 인덱스인 data를 바꿀때 사용하는 함수
React.useState(); 

// 배열접근 방식
const x = React.useState(0); 
const data = x[0];
const modifier = x[1];
// 배열 구조 분해 할당, 가독성 good!~
const [data, modifier] = React.useState(0);
// 어떤 값을 부여하던 modifier 함수는 그 값으로 리렌더링 함
// modifier를 통해 state를 변경할 때 컴포넌트가 재생성됨, 즉 새로운 값으로 UI에 반영

// useState 훅 사용시 state 직접 변경하는 건 올바르지 못함 
// why? 1.race condition 동시접근문제
const [data, modifier] = React.useState(false);
const changeValue = () => modifier(data);                   // 이렇게 접근 X
const changeValue = () => modifier((current) => !current);  // 이렇게 접근 해야함


```


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

### 공부하다 모르는 용어
##### 이벤트
이벤트란 웹 브라우저에서 DOM과 사용자가 interactive 하는 것
##### 이벤트 핸들러 
이벤트 핸들러란 특정요소에 이벤트를 처리하기 위한 함수

js의 이벤트핸들러 함수를 호출 시 첫번째 인자로 이벤트객체를 전달 받을 수 있음
호출한 함수안에서 preventDefault() 메서드 호출시 기본 동작 취소도 가능함

##### Hook
Hook 이란 함수 컴포넌트에서 ReactState와 lifecycle features를 연동 할수 있게 해줌
##### Lifecycle
Lifecycle이란 함수 컴포넌트에서 렌더링, 값변경, 삭제 시 특정 작업을 수행하게 함(useEffect?)
