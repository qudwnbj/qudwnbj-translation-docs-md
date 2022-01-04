# Query Functions

쿼리 함수는 말 그대로 **promise를 반환**하는 모든 함수가 될 수 있습니다. 반환되는 promise는 **데이터를 풀거나 오류를 발생시켜야** 합니다.

다음은 모두 유효한 쿼리 기능 구성입니다:

```js
useQuery(["todos"], fetchAllTodos);
useQuery(["todos", todoId], () => fetchTodoById(todoId));
useQuery(["todos", todoId], async () => {
  const data = await fetchTodoById(todoId);
  return data;
});
useQuery(["todos", todoId], ({ queryKey }) => fetchTodoById(queryKey[1]));
```

### 오류 발생 및 처리

React Query가 쿼리에 오류가 발생했는지 확인하려면 쿼리 함수가 **throw되어야** 합니다. 쿼리 함수에서 발생한 모든 오류는 쿼리의 오류 상태에서 지속됩니다.

```js
const { error } = useQuery(["todos", todoId], async () => {
  if (somethingGoesWrong) {
    throw new Error("Oh no!");
  }

  return data;
});
```

### 기본적으로 throw하지 않는 `fetch` 및 기타 클라이언트와 함께 사용

`axios` 또는 `graphql-request`와 같은 대부분의 유틸리티는 실패한 HTTP 호출에 대해 자동으로 오류를 발생시키는 반면, `fetch`와 같은 일부 유틸리티는 기본적으로 오류를 발생시키지 않습니다. 그런 경우에는 직접 throw해야 합니다. 다음은 널리 사용되는 `fetch` API를 사용하여 이를 수행하는 간단한 방법입니다:

```js
useQuery(["todos", todoId], async () => {
  const response = await fetch("/todos/" + todoId);
  if (!response.ok) {
    throw new Error("Network response was not ok");
  }
  return response.json();
});
```

### 쿼리 함수 변수

쿼리 키는 가져오는 데이터를 고유하게 식별하기 위한 것일 뿐만 아니라 쿼리 기능에 편리하게 전달되며 항상 필요한 것은 아니지만 필요한 경우 쿼리 기능을 추출할 수 있습니다:

```js
function Todos({ status, page }) {
  const result = useQuery(["todos", { status, page }], fetchTodoList);
}

// 쿼리 함수의 키, 상태 및 페이지 변수에 액세스합니다!
function fetchTodoList({ queryKey }) {
  const [_key, { status, page }] = queryKey;
  return new Promise();
}
```

### 변수 대신 쿼리 개체 사용

`[queryKey, queryFn, config]` 서명이 React Query의 API 전체에서 지원되는 곳이면 어디에서나 객체를 사용하여 동일한 구성을 표현할 수도 있습니다:

```js
import { useQuery } from "react-query";

useQuery({
  queryKey: ["todo", 7],
  queryFn: fetchTodo,
  ...config,
});
```

_last update : 2022.01.04_
