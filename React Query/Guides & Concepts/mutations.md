# Mutations

쿼리와 달리 mutations는 일반적으로 데이터를 생성/업데이트/삭제하거나 서버 부작용을 수행하는 데 사용됩니다. 이를 위해 React Query는 `useMutation` hook을 내보냅니다.

다음은 서버에 새 할 일을 추가하는 mutation의 예입니다:

```js
function App() {
  const mutation = useMutation((newTodo) => {
    return axios.post("/todos", newTodo);
  });

  return (
    <div>
      {mutation.isLoading ? (
        "Adding todo..."
      ) : (
        <>
          {mutation.isError ? (
            <div>An error occurred: {mutation.error.message}</div>
          ) : null}

          {mutation.isSuccess ? <div>Todo added!</div> : null}

          <button
            onClick={() => {
              mutation.mutate({ id: new Date(), title: "Do Laundry" });
            }}
          >
            Create Todo
          </button>
        </>
      )}
    </div>
  );
}
```

mutation은 주어진 순간에 다음 상태 중 하나만 있을 수 있습니다:

- `isIdle` 또는 `status === 'idle'` - mutation이 현재 유휴 상태이거나 새로/재설정된 상태입니다
- `isLoading` 또는 `status === 'loading'` - mutation이 현재 실행 중입니다
- `isError` 또는 `status === 'error'` - mutation에 오류가 발생했습니다
- `isSuccess` 또는 `status === 'success'` - mutation이 성공했으며 mutation 데이터를 사용할 수 있습니다

이러한 기본 상태 외에도 mutation 상태에 따라 더 많은 정보를 사용할 수 있습니다:

- `error` - mutation이 `error` 상태에 있으면 `error` 속성을 통해 오류를 사용할 수 있습니다.
- `data` - mutation이 `success` 상태에 있으면 `data` 속성을 통해 오류를 사용할 수 있습니다.

위의 예에서 **단일 변수 또는 객체**로 `mutate` 함수를 호출하여 mutation 함수에 변수를 전달할 수도 있음을 확인했습니다:

변수만 있는 mutations가 그렇게 특별한 것은 아니지만 `onSuccess` 옵션, [Query Client의 `invalidateQueries` 메소드](https://react-query.tanstack.com/reference/QueryClient#queryclientinvalidatequeries) 및 [Query Client의 `setQueryData` 메소드](https://react-query.tanstack.com/reference/QueryClient#queryclientsetquerydata)와 함께 사용하면 mutations는 매우 강력한 도구가 됩니다.
