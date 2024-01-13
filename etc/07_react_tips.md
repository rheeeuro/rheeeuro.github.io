---
layout: default
title: React Tips
nav_order: 7
parent: Etc
---

# 리액트 개발 다 뿌수기

## 1. useState

### 1.1 useState 왜 쓰나?

- 일반 변수 쓰면 리렌더링 안된다.
- vue의 ref랑 거의 동일
<details>
<summary>예시</summary>

```js
// 버튼 눌러도 그대로임
function App() {
  let count = 0;

  return (
    <div>
      <button onClick={() => {
        count++;
        }}>
   		증가
      </button>

      <h1>{ count }</h1>

      <button onClick={() => {
        count--;
        }}>
   		감소
      </button>
    </div>
  );
}
```

```js
// 버튼 누르면 리렌더링
function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <button onClick={() => {
        setCount(count + 1);
        }}>
   		증가
      </button>

      <h1>{ count }</h1>

      <button onClick={() => {
        setCount(count - 1);
        }}>
   		감소
      </button>
    </div>
  );
}
```

</details>

### 1.2 const?, let?

```js
let [count, setCount] = useState(0);
const [count, setCount] = useState(0);
```
useState를 쓸때 const를 쓰는 게 좋을 까 let을 쓰는게 좋을까?

const를 추천! 그냥 const 써라

### 1.3 useState 비동기 처리

- 대표적인 사례: API로 생성, 추가 및 삭제를 한 뒤 내부 state를 업데이트 하는 경우

```js
updateUser({name: "이상학", age: 30, authority: 'USER'})
  .then(response => {
    setUsers([
      ...users,
      response.data
    ])
  }).catch(error => {
    console.log(error);
  })
```

```js
updateUser({name: "이상학", age: 30})
  .then(prev => {
    setUsers([
      ...prev,
      response.data
    ])
  }).catch(error => {
    console.log(error);
  })
```
- 특정 값으로 업데이트 할 경우에는 값만 넣어줘도 무방하지만, 일부를 업데이트하는 경우 callback 함수로 넣어주는 것이 멘탈에 이롭다.


## 2. useEffect

### 2.1 useEffect

```
useEffect(function, depth)
```
- function: 수행하고자 하는 작업
- depth: 배열 형태이며, 배열 안에는 검사하고자 하는 특정 값 or 빈 배열
- vue의 watch랑 거의 동일!

### 2.2 componentDidMount

```js
useEffect(() => {
  // API 호출
  getUsers()
    .then(response => {
      setUsers(response.data);
    })
    .catch(error => {
      console.log(error);
    })
}, [])
```

### 2.3 componentWillUnmount

```js
useEffect(() => {

  // ...

  return () => {
    // 자원 반납
  }
}, [])
```

### 2.4 비동기 처리

- 처리가 안된 경우
```js
useEffect(() => {
  // API 호출
  getUsers()
    .then(response => {
      setUsers(response.data);
    })
    .catch(error => {
      console.log(error);
    })

  // 관리자 업데이트
  setAdminUsers(users.filter(user => {
    user.authority = "ADMIN";
  }))
}, [])
```

- 방법 1 (useEffect 사용)

```js
useEffect(() => {
  // API 호출
  getUsers()
    .then(response => {
      setUsers(response.data);
    })
    .catch(error => {
      console.log(error);
    })
}, [])

useEffect(() => {
  // 관리자 업데이트
  setAdminUsers(users.filter(user => {
    user.authority = "ADMIN";
  }))
}, [users])
```


- 방법 2 (async/await 사용)

```js
useEffect(async () => {
  // API 호출
  const response = await getUsers();
  
  // 유저 업데이트
  setUsers(response.data);

  // 관리자 업데이트
  setAdminUsers(response.data.filter(user => {
    user.authority = "ADMIN";
  }))
}, [])
```

- 방법 3 (callack 사용)

```js
useEffect(() => {
  // API 호출
  getUsers()
    .then(response => {
      setUsers(_ => {
        // 관리자 업데이트
        setAdminUsers(response.data.filter(user => {
          user.authority = "ADMIN";
          }))
        return response.data;
        });
    })
    .catch(error => {
      console.log(error);
    })
}, [])
```

## 3. 전역 상태 관리 라이브러리

### 1.1 Props drilling

![](https://miro.medium.com/v2/resize:fit:982/1*lNk3Eo8AqThYs68m465ADg.png)

### 1.2 Redux vs Recoil

- redux
> - redux 구조
> ![](https://velog.velcdn.com/images/fltxld3/post/f8bdc9f3-f8fa-42b8-a4ed-2a6c67aae842/image.png)
> - action, dispatcher, reducer, store등 러닝 커브가 높은 편
> - 여러가지 미들웨어와 조합하여 사용
> - 코드량이 많다

- recoil
> ![](https://velog.velcdn.com/images/fltxld3/post/01207cfd-6402-40df-be68-1ac18c5dc43c/image.png)
> atom과 selector만으로 어느정도 구현 가능. 러닝커브가 낮다.
> 직관적이며 간단한 구조
> devtool이 존재하지 않다 전역상태가 많은 경우 디버깅이 어려울 수 있다.
> vue의 pinia와 비슷함

## 4. css 프레임워크
- tailwindCSS를 적극 추천!
> - 팀 협업 과정에서 유리하다
> - utility-first class 기반
> - styled component와 같이 사용 가능
> - 반응형과 다크모드 구현에 매우매우 유리하다.
> - 조건부 스타일링에도 유리
> - intelliSense의 존재 
> - css에 익숙하지 않다면 러닝커브가 조금 있을수도...?