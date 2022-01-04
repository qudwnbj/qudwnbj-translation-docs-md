# Query Keys

핵심적으로 React Query는 쿼리 키를 기반으로 쿼리 캐싱을 관리합니다. 쿼리 키는 문자열처럼 단순할 수도 있고 많은 문자열과 중첩 개체의 배열처럼 복잡할 수도 있습니다. 쿼리 키가 직렬화 가능하고 **쿼리 데이터에 고유하다면** 사용할 수 있습니다!

### 문자열 쿼리 키

실제로 키의 가장 간단한 형태는 배열이 아니라 개별 문자열입니다. 문자열 쿼리 키가 전달되면 쿼리 키의 유일한 항목으로 문자열을 사용하여 내부적으로 배열로 변환됩니다. 이 형식은 다음에 유용합니다:

- 일반 목록/index 리소스
- 비계층적 리소스

```js
 // todo 리스트
 useQuery('todos', ...) // queryKey === ['todos']

 // 다른거 무엇이든!
 useQuery('somethingSpecial', ...) // queryKey === ['somethingSpecial']
```

### 배열 키

쿼리에 데이터를 고유하게 설명하기 위해 추가 정보가 필요한 경우 문자열이 있는 배열과 직렬화 가능한 개체를 사용하여 설명할 수 있습니다. 다음과 같은 경우에 유용합니다:

- 계층적 또는 중첩된 리소스
  - 항목을 고유하게 식별하기 위해 ID, index 또는 기타 primitive를 전달하는 것이 일반적입니다.
- 추가 변수가 있는 쿼리
  - 추가 옵션의 개체를 전달하는 것이 일반적입니다.

```js
// 개별 todo
 useQuery(['todo', 5], ...)
 // queryKey === ['todo', 5]

 // "preview" 형식의 개별 todo
 useQuery(['todo', 5, { preview: true }], ...)
 // queryKey === ['todo', 5, { preview: true }]

 // "done" 상태의 todo
 useQuery(['todos', { type: 'done' }], ...)
 // queryKey === ['todos', { type: 'done' }]
```

### 쿼리 키는 결정적으로 해시됩니다!

이 말은, 객체의 키 순서에 관계없이 다음 쿼리는 모두 동일한 것으로 간주됩니다:

```js
 useQuery(['todos', { status, page }], ...)
 useQuery(['todos', { page, status }], ...)
 useQuery(['todos', { page, status, other: undefined }], ...)
```

그러나 다음 쿼리 키는 같지 않습니다. 배열 항목 순서가 중요합니다!

```js
 useQuery(['todos', status, page], ...)
 useQuery(['todos', page, status], ...)
 useQuery(['todos', undefined, page, status], ...)
```

### 쿼리 기능이 변수에 의존하는 경우 쿼리 키에 포함합니다.

쿼리 키는 가져오는 데이터를 고유하게 설명하므로 쿼리 함수에서 **변경**하는 모든 변수를 포함해야 합니다. 예를 들어:

```js
function Todos({ todoId }) {
  const result = useQuery(["todos", todoId], () => fetchTodoById(todoId));
}
```

_last update : 2021.01.04_
