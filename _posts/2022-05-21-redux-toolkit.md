---
title: Redux Toolkit
author: royalbluee
date: 2022-05-21 09:00:00 -0500
categories: [Frontend]
tags: [Redux]
---

# 등장 배경

## Redux

리덕스는 `Flux 아키텍처`의 구현체로 대형 MVC 애플리케이션에서 종종 나타나는 데이터 간 의존성 이슈, 즉 연쇄적인 갱신이 뒤얽혀 데이터의 흐름을 예측할 수 없게 만들었던 문제를 해결하기 위해서 고안되었습니다.

리덕스를 사용하는 구조에서는 전역 상태를 전부 하나의 `저장소(store)` 안에 있는 객체 트리에 저장합니다. 그리고 상태를 변경하는 것은 어떤 일이 일어날지 서술하는 객체인 `액션(action)`을 `내보내는(dispatch)` 것이 유일한 방법입니다. 마지막으로 액션이 전체 애플리케이션의 상태를 어떻게 변경할지 명시하기 위해서는 `리듀서(reducer)`의 작성이 필요합니다.

`리듀서(reducer)`는 변화를 일으키는 함수로써 전달받은 액션을 가지고 새로운 상태를 만들어서 스토어에 전달합니다. 이 모든 설계는 데이터가 단방향으로 흐른다는 전제하에 데이터의 일관성을 향상시키고 버그 발생원인을 더 쉽게 파악하려는 의도에서 출발했음을 알게 되었습니다.

완벽할 것만 같았던 리덕스에도 문제가 있었습니다. 대표적으로 언급되는 리덕스의 3가지 문제는 아래와 같습니다.

- 리덕스 스토어 환경 설정은 너무 복잡하다!
- 리덕스를 유용하게 사용하려면 많은 패키지를 추가해야 한다!
- 리덕스는 보일러플레이트, 즉 어떤 일을 하기 위해 꼭 작성해야 하는 (상용구)코드를 너무 많이 요구한다!

이러한 이슈를 해결하기 위해 리덕스 툴킷이 등장합니다.

# 소개

RTK는 어떻게 이전의 리덕스 라이브러리가 가진 복잡함을 단순화 시킬 수 있던 것일까요? 아래부터는 RTK에서 제공하는 API를 예제와 함께 살펴보고자 합니다.

## configureStore()

스토어를 구성하는 함수입니다. `configureStore`는 리덕스 라이브러리의 표준 함수인 createStore를 추상화한 것입니다.

```javascript
import { configureStore } from "@reduxjs/toolkit";

import rootReducer from "./reducers";

const store = configureStore({ reducer: rootReducer });
```

`configureStore` 함수는 `reducer`, `middleware`, `devTools`, `preloadedState`, `enchancer` 정보를 전달합니다.

- reducer: 리듀서에는 단일 함수를 전달하여 스토어의 루트 리듀서(root reducer)로 바로 사용할 수 있습니다. 또한 슬라이스 리듀서들로 구성된 객체를 전달하여 루트 리듀서를 생성하도록 할 수 있습니다. 이런 경우에는 내부적으로 기존 리덕스 combineReducers 함수를 사용해서 자동적으로 병합하여 루트 리듀서를 생성합니다.
- middleware: 기본적으로는 리덕스 미들웨어를 담는 배열입니다. 사용할 모든 미들웨어를 배열에 담아서 명시적으로 작성할 수도 있습니다. 그렇지 않으면 getDefaultMiddleware를 호출하게 됩니다. 사용자 정의, 커스텀 미들웨어를 추가하면서 동시에 리덕스 기본 미들웨어를 사용할 때 유용한 방법입니다.
- devTools: 불리언값으로 리덕스 개발자 도구를 끄거나 켭니다.

## createSlice()

리덕스 로직을 작성하는 표준 접근법은 `createSlice`를 사용하는 것에서 출발합니다.

`createSlice`에 선언된 슬라이스 이름을 따라서 리듀서와 그리고 그것에 상응하는 액션 생성자와 액션 타입을 자동으로 생성합니다. 따라서 `createSlice`를 사용하면 따로 `createAction`, `createReducer`를 작성할 필요가 없습니다.

공식 문서의 리덕스 스타일 가이드에 따르면 슬라이스 파일은 `feature` 폴더 안에서 상태 도메인 별로 나누어 정리하고 있습니다.

```javascript
// features/counter/counterSlice.js
import { createSlice } from "@reduxjs/toolkit";

const initialState = {
  value: 0,
};

export const counterSlice = createSlice({
  name: "counter",
  initialState,
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;

export default counterSlice.reducer;
```

# 마무리

위 내용을 짧게 정리해 보면 다음과 같습니다.

- 리덕스는 데이터를 단방향으로 흐르게 하여 결과를 예측 가능하게 하고 디버깅을 쉽게 만든다.
- RTK는 기존 리덕스의 문제를 개선하고, 리덕스 로직을 작성하는 표준을 제안한다.
  - 스토어 구성은 `configureStore`를 사용한다.
  - 리덕스 로직을 작성할 때는 `createSlice`를 사용한다.
