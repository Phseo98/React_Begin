# React
React는 사용자 인터페이스 구축을 하기위해 효율적이고 유연한 js 라이브러리다. 

### 특징
1. Virtual DOM - Virtual Dom을 사용하여 변경된 부분만 DOM에 적용되 업데이트 되기 때문에 효율적임
2. component 기반 구조
3. 단방향 데이터 흐름 - 상위 컴포넌트에서 하위 컴포넌트로 한방향으로 흐리기 때문에 데이터 예측, 디버깅하기 효율적임
4. JSX문법
5. Single Page Application

### Virtual DOM 
컴포넌트가 렌더링 되면 DOM의 복제본을 메모리에 생성하고, 컴포넌트에 변경된 부분이 있으면 DOM과 복제본 DOM을 비교해, 변경된 부분만 DOM에 반영되어 렌더링 됨

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
- 리액트 컴포넌트들은 인자를 받음 

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

// props는 object 형태로 전달되기 때문에 인자에 객체로도 받을수 있음
function ChildComponent({message}) {
  return <p>{message}</p>;
}

// 컴포넌트가 React.memo()로 래핑되면 부모 컴포넌트로 부터 자식컴포넌트에게 데이터를 전달할때 메모이징 할수 있다
const Memoizing = React.memo(ChildComponent);
// 부모컴포넌트로 부터 자식컴포넌트에게 데이터를 전달할때 타입을 확인 할수 없기 떄문에 
// 타입에러가 생기지 않음 그래서 propTypes사용
// propTypes을 사용하면 타입을 지정하여 에러를 표시해줌
```

### useEffect
- state가 변화 할때마다 컴포넌트가 reder되면 매우 비효율적일 수 있음
- when? api를 통해서 데이터가져올때 
- why? state 변화가 있을떄 마다 재랜더링 되는 특징이 있는데 api 호출해서 데이터를 가져오면 불필요한 부분도 재랜더링 되고 랜더링 될때마다 api 호출 하기때문에 비효율적임
- 렌더링 관리를 위해 useEffect 사용
- 내가 원할떄 코드를 실행할 수 있음


``` javascript
import { useState, useEffect  } from 'react';
import Button from './Button';

function App() {
  const[counter, setCounter] = useState(0);
  const[keyword, setKeyword] = useState("");
  const onClick = () => setCounter((prev) => prev + 1);
  const onChange = (event) => setKeyword(event.target.value);
  useEffect(() => {
    console.log("I run only once.")
  }, []); // [] 안에는 react가 변화하는걸감지, 빈배열이면 한번만 실행되는 이유
  useEffect(() => {
     console.log("I run when 'keyword' Changes");
  }, [keyword]); // keyword가 변화할때 코드실행  변수에의존 한다 (의존성)
  useEffect(() => {
    console.log("I run when 'counter' Changes");
 }, [counter]); // counter가 변화할때 코드실행 
  useEffect(() => {
  console.log("I run when 'counter' and 'keyword' Changes");
}, [counter, keyword]); // counter,keyword가 변화할때 코드실행 

  // Clean Up function
  // Clean Up 함수는 컴포넌트가 unMount될때 실행됨
  useEffect(() => { 
      console.log("createded :)"); // Mount 될때 호출
      return () => console.log("distoried :("); // Mount 해제 될때 호출
  }, []);
  return (
    <div>
      <input 
        value={keyword}
        onChange={onChange}
        type="text" 
        placeholder="Search here.." />
      <h1>{counter}</h1>
      <button onClick={onClick}>click me!</button>
     </div>
  );
}

export default App;
```


### 공부하다 모르는 용어
#### 이벤트
이벤트란 웹 브라우저에서 DOM과 사용자가 interactive 하는 것
#### 이벤트 핸들러 
이벤트 핸들러란 특정요소에 이벤트를 처리하기 위한 함수

js의 이벤트핸들러 함수를 호출 시 첫번째 인자로 이벤트객체를 전달 받을 수 있음
호출한 함수안에서 preventDefault() 메서드 호출시 기본 동작 취소도 가능함

#### Hook
Hook 이란 함수 컴포넌트에서 ReactState와 lifecycle features를 연동 할수 있게 해줌
#### Lifecycle
Lifecycle이란 함수 컴포넌트에서 렌더링, 값변경, 삭제 시 특정 작업을 수행하게 함(useEffect?)

#### Memoizing
Memoizing이란 이전 값이랑 새로 계산되는 값이랑 동일하면 수행 하지않음

#### Mount
Mount란 컴포넌트가 DOM에 삽입되고 나서 화면에 나타날때를 의미함