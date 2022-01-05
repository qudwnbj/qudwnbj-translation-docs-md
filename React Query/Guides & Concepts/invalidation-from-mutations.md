# Invalidation from Mutations

쿼리 무효화는 고비의 절반입니다. 그것들을 무효화할 **때**를 아는 것은 나머지 절반입니다. 일반적으로 앱의 mutation이 성공하면 mutation의 새로운 변경 사항을 설명하기 위해 무효화하고 다시 가져와야 하는 관련 쿼리가 애플리케이션에 있을 가능성이 **매우** 높습니다.

예를 들어, 새로운 할 일을 게시하는 mutation이 있다고 가정합니다:

```js
const mutation = useMutation(postTodo);
```

성공적인 `postTodo` mutation이 발생하면 모든 `todos` 쿼리가 무효화되고 새 할일 항목을 표시하기 위해 refetch할 수 있습니다. 이렇게 하려면 `useMutation`의 `onSuccess` 옵션과 `client`의 `invalidateQueries` 기능을 사용할 수 있습니다.

```js
import { useMutation, useQueryClient } from "react-query";

const queryClient = useQueryClient();

// When this mutation succeeds, invalidate any queries with the `todos` or `reminders` query key
const mutation = useMutation(addTodo, {
  onSuccess: () => {
    queryClient.invalidateQueries("todos");
    queryClient.invalidateQueries("reminders");
  },
});
```

[`useMutation` hook](https://github.com/qudwnbj/qudwnbj-translation-docs-md/blob/master/React%20Query/Guides%20%26%20Concepts/mutations.md)에서 사용 가능한 콜백을 사용하여 무효화를 연결할 수 있습니다.

_last update : 2022.01.05_
