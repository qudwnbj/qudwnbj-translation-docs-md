# Dependent Queries

종속(또는 직렬) 쿼리는 실행하기 전에 완료해야 하는 이전 쿼리에 의존합니다. 이를 달성하기 위해 `enable` 옵션을 사용하여 쿼리를 실행할 준비가 되었음을 알리는 것처럼 쉽습니다.

```js
// 유저 불러오기
const { data: user } = useQuery(["user", email], getUserByEmail);

const userId = user?.id;

// 그리고나서 유저 프로젝트 불러오기
const { isIdle, data: projects } = useQuery(
  ["projects", userId],
  getProjectsByUser,
  {
    // 이 쿼리는 유저 id가 존재할때까지 실행되지 않습니다.
    enabled: !!userId,
  }
);

// isIdle은 `enabled`가 true이고 쿼리가 fetch를 시작할 때까지 `true`입니다.
// 그런 다음 `isLoading` 단계로 이동하고 바라건대 `isSuccess` 단계로 이동합니다. :)
```

_last update : 2022.01.05_
