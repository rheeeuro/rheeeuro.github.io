---
layout: default
title: Tailwind Styled Components
nav_order: 8
parent: Etc
---

# Tailwind Styled Components

## 1. CSS 문제점

프로젝트의 규모와 복잡도가 점점 커져가며 함께 협업하는 팀원 수도 많아지면서 일관된 패턴이 없는 CSS 작성은 큰 문제가 되었다. 더불어 다양한 디바이스들의 등장으로 CSS  점점 복잡해지게 되었습니다. 이러한 문제점들을 해결하기 위해 등장한 것이 CSS 전처리기 입니다.

CSS가 구조적으로 작성될 수 있게 도움을 주는 도구인 CSS 전처리기이지만 이 자체만으로는 웹 서버가 인지하지 못하기 때문에 각 CSS 전처리기에 맞는 Compiler을 사용해야 하며 컴파일을 통해 우리가 사용하는 CSS 문서로 변환하게 됩니다.

문제는, 
CSS 전처리기를 이용해서 이전의 문제점들을 해결하기 위해 단순히 계층 구조를 만들어 내는 것에 의지하게 되었고 이는 CSS 파일의 용량을 과대하게 키우게 되었습니다.

위의 CSS 전처리기 문제를 보완하기 위해 BEM / OOCSS / SMACSS 같은 CSS 방법론이 등장하였으나 이 세 방법론 모두 동일한 지향점을 가지고 있습니다.

- 코드의 재사용
- 코드의 간결화(유지 보수 용이)
- 코드의 확장성
- 코드의 예측성(클래스 명으로 의미 예측)

하지만, 위 방법론도 해결하지 못한 캡슐화 불가로 인한 장황한 class 명의 문제를 보완하기 위해 CSS 도 컴포넌트 영역으로 불러오기 위한 CSS-In-JS 가 등장하였습니다. 대표적으로 Styled-Component가 있으며 기능적 / 상태를 가진 컴포넌트들로부터 UI 를 완전히 분리해 사용할 수 있는 아주 단순한 패턴을 제공합니다.

※ 각종 CSS 방법론의 특징과 장단점 ※
||특징|장점|단점|
|---|---|---|---|
|CSS|기본 스타일링 방법|-|일관된 패턴을 갖기 어려움,<br/>!important의 남용|
|SASS<br/>(preprocessor)|프로그래밍 방법론을 도입하여,<br/>컴파일된 CSS를 만들어내는 전처리기|변수/함수/상속 개념을 활용하여 재사용 가능<br/>CSS의 구조화|전처리 과정이 필요.<br/>디버깅의 어려움이 있음.<br/>컴파일한 CSS파일이 거대해짐|
|BEM|CSS 클래스명 작성에 일관된 패턴을 강제하는 방법론|네이밍으로 문제 해결,<br/>전처리 과정 불필요|선택자의 이름이 장황하고,<br/>클래스 목록이 너무 많아짐|
|Styled-Component<br/>(Css-in-JS)|컴포넌트 기반으로 CSS를 작성할 수 있게 도와주는 라이브러리|CSS를 컴포넌트 안으로 캡슐화,<br/>네이밍이나 최적화를 신경 쓸 필요가 없음|빠른 페이지 로드에 불리함|

`[참고]https://kg-dlife.tistory.com/191`

## 2. Styled Components

```js
import styled from "styled-components";

const Btn = styled.button`
  background: ${(props) => props.bg};
  color: black;
  padding: 10px;
`;

function Detail() {
  return (
    <div>
      <Btn bg="red">버튼</Btn>
      <Btn bg="blue">버튼</Btn>
    </div>
  );
}
```

### 장점

- 컴포넌트 단위의 스타일링
- 조건부 스타일링
- 확장 스타일링
- 중첩 스코프

### 단점

- 빠른 페이지 로드에 불리하다
- 여전히 협업에서 불리하다

## 3. TailwindCSS

```js
<button class="py-2 px-4 rounded-lg shadow-md text-white bg-blue-500">Click me</button>
```

## 4. TailwindCSS + Styled Components

```js
import styled from "styled-components";
import tw from "twin.macro";

const Heading = styled.h1`
  ${tw`font-bold text-4xl text-blue-100 font-sans`}
`;
```

### 장점

- CSS작성에 시간을 줄일 수 있다
- 코드의 전체적인 길이를 줄일 수 있다.
- 커스터마이징이 쉬워 원하는대로 변경할 수 있다.
- 반응형, 다크모드 구현이 매우 유리하다.
- 협업에도 유리하다

### 단점

- 초반 러닝커브가 있다.
- tailwind 적용이 어려운 스타일이 존재할 수 있다.
- 클래스 이름 길이의 증가로 컴포넌트의 가독성이 안좋아진다

## 5. Tailwind Styled Components

```
import tw from "tailwind-styled-components";

const Input = tw.input`
    w-60
    border-blue-300
    border
    rounded-xl
`;

const Button = tw.button`
    w-60
    p-2
    bg-indigo-600
    rounded-xl
    text-white
`;
```
