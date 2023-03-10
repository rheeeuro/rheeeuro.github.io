---
layout: default
title: React Component
nav_order: 2
parent: Etc
---

# React 클래스형과 함수형 차이 (_21.12.08_)

리액트를 사용하여 프론트 개발을 할 떄 두 가지 방법으로 컴포넌트를 선언할 수 있다.  
과거에는 클래스형 컴포넌트를 주로 사용했지만, 2019년 v16.8부터 함수형 컴포넌트에 리액트 훅(hook)을 지원해주어서 현재는 공식 문서에 **`함수형 컴포넌트와 훅을 함께 사용할 것을 권장`** 하고 있다.

## 1. 컴포넌트

> ### 함수형 컴포넌트 (Stateful 컴포넌트)
>
> ```
> import React from 'react';
> import './App.css';
>
> function App() {
>   const name = 'react';
>   return <div className = "react">{name}</div>
> }
>
> export default App;
> ```
>
> ### 클래스형 컴포넌트 (Stateless 컴포넌트)
>
> 포넌트 상속을 받아야 하며 render 메서드가 반드시 있어야 한다. (보여주어야 할 JSX를 반환해야 한다.)
>
> ```
> import React, {Component} from 'react';
>
> class App extends Component {
>   render() {
>     const name = 'react';
>     return <div className="react">{name}</div>
>   }
> }
>
> export default App;
> ```
>
> <br/>
> <br/>

## 2. 일반적 차이

> | 항목                            | 클래스형                     | 함수형                         |
> | ------------------------------- | ---------------------------- | ------------------------------ |
> | state, lifeCycle 관련 기능 사용 | 가능                         | 불가능 (Hook을 통해 해결 가능) |
> | 메모리 자원 사용                | 조금 더 많이 사용            | 덜 사용                        |
> | 특징                            | 임의 메서드를 정의할 수 있음 | 캄포넌트 선언이 편함           |
>
> <br/>

## 3. 기능: state 사용 차이

> state: 컴포넌트 내부에서 바뀔 수 있는 값
>
> ### 클래스형
>
> - constructor안에서 this.state 초기 값 설정 가능
> - constructor없이 바로 state 초기 값을 설정할 수 있다.
> - 클래스형 컴포넌트의 state는 객체 형식
> - this.setState함수로 state의 값을 변경할 수 있다.
>
> ### 함수형
>
> - 함수형 컴포넌트에서는 useState 함수로 state를 사용한다.
> - **`useState함수를 호출하면 현재상태, 상태를 바꾸어 주는 함수의 배열이 반환`** 된다.
>
> ```
> const [message, setMessage] = useState('');
> ```
>
> <br/>
> <br/>

## 4. props 사용 차이

> props
>
> - 컴포넌트의 속성을 설정할 때 사용하는 요소
> - **`읽기 전용`**
> - 컴포넌트 자체 props를 수정해서는 안된다.
> - 모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수함수처럼 동작해야 한다.
> - 수정되는 것은 state이다.
>
> ### 클래스형 컴포넌트의 props
>
> - this.props를 통해 값을 불러올 수 있다.
> - 부모 객체의 키 값, 자식 props 사용
>
> ### 함수형 컴포넌트의 props
>
> - props를 불러올 필요없이 바로 호출할 수 있다. (인자로 받기 때문)
>   <br/>

## 5. 이벤트 핸들링

> ### 클래스형 컴포넌트에서 이벤트 핸들링
>
> - 함수 선언 시 에로우 함수로 바로 선언 가능하다.
> - 요소에 적용하기 위해서는 this를 붙여야 한다.
>   <br/>

## 6.그 이외의 차이점

> - ### 함수형 컴포넌트는 렌더링된 값들을 고정시킨다.
>   > **`클래스형 컴포넌트에서 props는 불변의 값이지만 this는 변경 가능하고 조작할 수 있다`**.  
>   > 따라서 요청이 진행되고 있는 상황에서 클래스 컴포넌트가 다시 렌더링 된다면 this.props 또한 바뀐다.  
>   > 만약 UI가 현재 애플리케이션의 상태를 보여주는 함수라 한다면, 이벤트 핸들러 또한 시각적 컴포넌트와 같이 렌더링 결과의 한 부분인 것이다.  
>   > 즉 이벤트 핸들러가 어떤 props와 state를 가진 render에 종속된다는 것이다.
>   > 따라서 클래스형 매서드에서는 props값을 render될 때의 값으로 고정해둘 필요가 있다. (클로저 방식)
>   >
>   > ```
>   > class ProfilePage extends React.Component {
>   >   render() {
>   >     // props의 값을 고정!
>   >     const props = this.props;
>   >
>   >     // Note: 여긴 *render 안에* 존재하는 곳이다!
>   >     // 클래스의 메서드가 아닌 render의 메서드
>   >     const showMessage = () => {
>   >       alert('Followed ' + props.user);
>   >     };
>   >
>   >     const handleClick = () => {
>   >       setTimeout(showMessage, 3000);
>   >     };
>   >
>   >     return <button onClick={handleClick}>Follow</button>;
>   >   }
>   > }
>   > ```
>   >
>   > <br/>   
>   > <br/>

## + 참고

> ### 일반함수와 화살표함수의 차이
>
> ```
> function BlackDog() {
>   this.name = '어피치';
>   return {
>     name: '라이언',
>     sayHello: function() {
>       console.log(this.name + ': 안녕!');
>     }
>   }
> }
>
> const blackDog = new Blackdog();
> blackDog.sayHello(); // 라이언: 안녕!
>
> function WhiteDog() {
>   this.name = '어피치';
>   return {
>     name: '라이언',
>     sayHello: () => {
>       console.log(this.name + ': 안녕!');
>     }
>   }
> }
>
> const whiteDog = new Whitedog();
> whiteDog.sayHello(); // 어피치: 안녕!
> ```
>
> function()을 사용하면 라이언이 나타나고, () => {} 를 사용하면 어피치가 나타난다.  
> **`일반 함수는 자신이 종속된 객체를 this로 가리키며, 화살표 함수는 자신이 종속된 인스턴스를 가리킨다`**.
