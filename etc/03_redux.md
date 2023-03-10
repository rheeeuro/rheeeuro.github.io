---
layout: default
title: React Component
nav_order: 2
parent: Etc
---

# Redux(_21.12.06_)

<img src="https://media.github.kakaocorp.com/user/8666/files/7bc6b136-e65d-402c-9a53-33adeaa13232" width="30%">

---

## 1. Redux란?

- Redux는 기본적으로 Javascript appliation들의 state(상태)를 관리하는 방법이다. (React가 아니라 Javascript이다)
- Redux는 사람들이 React와 많이 사용해서 유명해졌지만, React와 Redux는 별개이다.
- Redux는 Angular, Vue, Vanilla JS등 Javascript를 사용하는 모든 곳에 쓸 수 있다.
- 컴포넌트들의 상태관리 관련 로직들을 다른 파일들로 분리시켜서 더욱 효율적으로 관리할 수 있으며 글로벌 상태 관리도 쉽게 할 수 있다.

---

## 2. 상태 관리도구의 필요성

- 상태란: React에서 state는 컴포넌트 안에서 관리되는 것이다. (Redux가 전역변수를 만들어주는 느낌)
- Component간의 정보 공유: 자식 컴포넌트 간의 데이터를 주고받을 때는 상태를 관리하는 부모 컴포넌트를 통해서 주고 받는다. (자식이 많아지면 상태관리가 매우 복잡해진다.)
- [Props drilling](https://www.geeksforgeeks.org/what-is-prop-drilling-and-how-to-avoid-it/) 이슈: 상태를 관리하는 상위 컴포넌트에서 계속 내려받아야 한다.
- 상태관리 툴을 이용하여 전역 상태 저장소 제공 (React Context, Redux, MobX)

---

## 3. Redux의 기본 개념

### 1. Single source of truth

> 동일한 데이터는 항상 같은 곳에서 가지고 온다. (스토어라는 하나뿐인 데이터 공간)

### 2. State is read-only

> 리액트에서 setState 메서드를 사용해야만 상태 변경이 가능하다.  
> 리덕스에서도 액션이라는 객체를 통해서만 상태를 변경할 수 있다.

### 3. Changes are made with pure functions

> 변경을 순수함수로만 가능하다.  
> 리듀서와 연관되는 내용이다.  
> Store(스토어) - Action(액션) - Reducer(리듀서)  
> <img src="https://i2.wp.com/hanamon.kr/wp-content/uploads/2021/07/%E1%84%85%E1%85%B5%E1%84%83%E1%85%A5%E1%86%A8%E1%84%89%E1%85%B3-%E1%84%89%E1%85%A1%E1%86%BC%E1%84%90%E1%85%A2%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%B5-%E1%84%83%E1%85%A1%E1%86%AB%E1%84%80%E1%85%A8.png?w=919&ssl=1" width="50%">

> - Store(스토어): 스토어는 상태가 관리되는 오직 하나의 공간이다.
>   > - store를 생성하고 reducer를 연결하여 어플리케이션에 연결하게 된다.
>   >
>   > ```
>   > import { createStore } from 'redux';
>   > import todoApp from './reducers';
>   > let store = createStore(todoApp);
>   > ```
> - Action(액션): 액션은 앱에서 스토어에 운반할 데이터를 말한다. (주문서. 자바스크립트 객체 형식)
>   > - 액션의 type은 일반적으로 문자열 상수로 정의된다. 정의된 action type은 action creator(액션 생성자)를 통해 사용된다.
>   >
>   > ```
>   >    const ADD_TO_DO = 'ADD_TODO' // action의 type을 정의
>   >
>   >    // 액션 생성자
>   >    function addToDo(text) {
>   >        return {
>   >            type: ADD_TODO,
>   >            text
>   >        }
>   >    }
>   > ```
> - Reducer(리듀서):액션을 스토어에 바로 전달하지 않고 dispatch() 메서드를 이용해 리듀서에 전달한다. 리듀서가 주문을 보고 스토어의 상태를 업데이트 하는 것이다. (데이터를 한 방향으로 흘러가게 하기 위함)
>   > - 액션을 통해 어떠한 행동을 정의했다면, 그 결과 어플리케이션의 상태가 어떻게 바뀌는지를 특정하게 되는 함수이다.
>   >
>   > ```
>   >  function toDoApp(state=initialState, action){
>   >      switch(action.type):
>   >          case SET_VISIBILITY_FILTER:
>   >              return Object.assign({}, state, {
>   >                  visibilityFilter: action.filter
>   >              });
>   >          default:
>   >              return state
>   >  }
>   > ```

---

## 4. 리덕스의 장점

- 상태를 예측 가능하게 만든다.
- 유지보수
- 디버깅에 유리
- 테스크를 붙이기 용이

---

## 5. Flux 구조

[Flux](https://facebook.github.io/flux/docs/in-depth-overview/)는 Facebook에서 만든 client-side web application을 구축할 때 사용하는 application architcture(앱 구조), design pattern(디자인 패턴)이다. 대규모 프로젝트에서 [MVC(Model-View-Controller)](https://developer.mozilla.org/ko/docs/Glossary/MVC)가 너무 복잡해지는 단점을 보완하는 단방향 데이터 흐름(undirectional data flow)의 구조이다.  
물론 차이점이 있지만, 결론적으로 Flux, 리덕스 두 가지의 구조 모두 닮았으며 결국 리덕스는 Flux 패턴을 좀 더 쉽고 정돈된 형태로 쓸 수 있게 도와주는 라이브러리라고 볼 수 있다.
<img src="https://miro.medium.com/max/1276/1*oRBseHE_yxtlbcRTrbkRnQ.png" width="70%">

---

## 6. Redux를 사용하는 것과 Context API를 사용하는 것의 차이

### 1. 미들웨어

리덕스에는 [미들웨어(Middleware)](https://ko.wikipedia.org/wiki/%EB%AF%B8%EB%93%A4%EC%9B%A8%EC%96%B4)라는 개념이 존재한다. 리덕스의 미들웨어를 사용하면 액션 객체가 리듀서에서 처리되기 전에 원하는 작업들을 수행할 수 있다.  
_(ex. 특정 조건에 따라 액션 무시, 액션을 콘솔에 출력하거나 서버쪽에 로깅, 액션이 디스패치 되었을때 수정하여 리듀서에게 전달, 특정 액션이 발생했을 때 다른 액션 발생 등등)_

### 2. 유용한 함수와, Hooks

Context, Provider 설정, 커스텀 Hooks 등을 직접 만들지 않고 내부 함수를 이용해 손쉽게 상태를 조회하거나 액션을 디스패티 할 수 있다. (함수 내부적으로 최적화도 잘 되어 있다.)

### 3. 하나의 커다란 상태

[Context API](https://react.vlpt.us/basic/22-context-dispatch.html) 를 사용해서 글로벌 상태 관리를 할 때에는 일반적으로 기능별로 Context를 만들어서 사용하는 것이 일반적이다. 반면 리덕스에서는 모든 글로벌 상태를 하나의 커다란 상태 객체에 넣어서 사용하는 것이 필수이다. 때문에 매번 Context를 새로 만드는 수고로움을 덜 수 있다.

### **따라서 리덕스는 프로젝트 규모가 크고 비동기 작업을 자주 하게 되는 프로젝트에 적합하다.**

---

## 7. React Saga

TODO: https://min9nim.vercel.app/2020-04-23-redux-saga/ 정리
