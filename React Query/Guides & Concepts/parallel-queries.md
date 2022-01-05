# Parallel Queries

"병렬" 쿼리는 병렬로 실행되거나 동시에 fetching의 동시성을 최대화하기 위해 실행되는 쿼리입니다.

## 수동 병렬 쿼리

병렬 쿼리의 수가 변경되지 않으면 병렬 쿼리를 사용하기 위한 **추가 노력이 없습니다**. React Query의 `useQuery`와 `useInfiniteQuery` hooks를 원하는 만큼 나란히 사용하세요!

```js
function App () {
   // 다음 쿼리는 병렬로 실행됩니다.
   const usersQuery = useQuery('users', fetchUsers)
   const teamsQuery = useQuery('teams', fetchTeams)
   const projectsQuery = useQuery('projects', fetchProjects)
   ...
 }
```

> 서스펜스 모드에서 React Query를 사용할 때 이 병렬 처리 패턴은 작동하지 않습니다. 첫 번째 쿼리가 내부적으로 약속을 던지고 다른 쿼리가 실행되기 전에 구성 요소를 일시 중단하기 때문입니다. 이 문제를 해결하려면 `useQueries` hooks(권장됨)를 사용하거나 각 `useQuery` 인스턴스에 대해 별도의 구성 요소를 사용하여 고유한 병렬 처리를 조정해야 합니다(이는 재미없다).

## `useQueries`를 사용한 동적 병렬 쿼리

실행해야 하는 쿼리 수가 렌더링에서 렌더링으로 변경되는 경우 hooks 규칙을 위반하므로 수동 쿼리를 사용할 수 없습니다. 대신 React Query는 원하는 만큼 병렬로 동적으로 쿼리를 실행하는 데 사용할 수 있는 `useQueries` hooks를 제공합니다.

`useQueries`는 **쿼리 옵션 객체의 배열**을 허용하고 **쿼리 결과의 배열**을 반환합니다:

```js
function App({ users }) {
  const userQueries = useQueries(
    users.map((user) => {
      return {
        queryKey: ["user", user.id],
        queryFn: () => fetchUserById(user.id),
      };
    })
  );
}
```
