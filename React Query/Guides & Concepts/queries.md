# Queries

### 기본 쿼리

쿼리는 **고유 키**에 연결된 비동기 데이터 소스에 대한 선언적 종속성입니다. 쿼리는 서버에서 데이터를 가져오기 위해 모든 Promise 기반 메서드(GET 및 POST 메서드 포함)와 함께 사용할 수 있습니다. method가 서버의 데이터를 수정하는 경우 쿼리 대신 [Mutations](https://github.com/qudwnbj/qudwnbj-translation-docs-md/blob/master/React%20Query/Guides%20%26%20Concepts/mutations.md)를 사용하는 것이 좋습니다.

components 또는 custom hooks에서 쿼리를 구독하려면 최소한 다음을 사용하여 `useQuery` 후크를 호출하십시오:

- **쿼리의 고유 키**
- 다음과 같은 promise을 반환하는 함수:
  - 데이터를 풀거나
  - 에러를 던지는 함수

```js
import { useQuery } from "react-query";

function App() {
  const info = useQuery("todos", fetchTodoList);
}
```

제공한 **고유 키**는 애플리케이션 전체에서 쿼리를 다시 가져오고, 캐싱하고, 공유하는 데 내부적으로 사용됩니다.

`useQuery`에서 반환한 쿼리 결과에는 템플릿 및 기타 데이터 사용에 필요한 쿼리에 대한 모든 정보가 포함되어 있습니다:

```js
const result = useQuery("todos", fetchTodoList);
```

`result` object에는 생산적으로 인식해야 하는 몇 가지 매우 중요한 상태가 포함되어 있습니다. 쿼리는 주어진 순간에 다음 상태 중 하나일 수 있습니다:

- `isLoading` 또는 `status === 'loading'` - 쿼리에 데이터가 없고 현재 가져오는 중입니다.
- `isError` 또는 `status === 'error'` - 쿼리에 오류가 발생했습니다.
- `isSuccess` 또는 `status === 'success'` - 쿼리가 성공했으며 데이터를 사용할 수 있습니다.
- `isIdle` 또는 `status === 'idle'` - 쿼리가 현재 비활성화되어 있습니다(이에 대해 조금 더 배우게 될 것입니다).

이러한 기본 상태 외에도 쿼리 상태에 따라 더 많은 정보를 사용할 수 있습니다:

- `error` - 쿼리가 `isError` 상태인 경우 `error` 속성을 통해 오류를 사용할 수 있습니다.
- `data` - 쿼리가 `success` 상태인 경우 `data` 속성을 통해 데이터를 사용할 수 있습니다.
- `isFetching` - 어떤 상태에서든 쿼리가 언제든지 가져오는 경우 `isFetching`은 `true`입니다.(백그라운드 다시 가져오기 포함)

**대부분**의 쿼리의 경우 일반적으로 `isLoading` 상태를 확인한 다음 `isError` 상태를 확인한 다음 마지막으로 데이터를 사용할 수 있다고 가정하고 성공적인 상태를 렌더링하는 것으로 충분합니다:

```js
function Todos() {
  const { isLoading, isError, data, error } = useQuery("todos", fetchTodoList);

  if (isLoading) {
    return <span>Loading...</span>;
  }

  if (isError) {
    return <span>Error: {error.message}</span>;
  }

  // 이 시점에서 `isSuccess === true`라고 가정할 수 있습니다.
  return (
    <ul>
      {data.map((todo) => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  );
}
```

boolean 값이 마음에 들지 않으면 언제든지 `status` state도 사용할 수 있습니다:

```js
function Todos() {
  const { status, data, error } = useQuery("todos", fetchTodoList);

  if (status === "loading") {
    return <span>Loading...</span>;
  }

  if (status === "error") {
    return <span>Error: {error.message}</span>;
  }

  // 이것 또한 status === 'success' 이지만, "else"를 사용한 구조도 정상 작동합니다.
  return (
    <ul>
      {data.map((todo) => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  );
}
```

_last update : 2021.01.04_
