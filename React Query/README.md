![React Query](https://react-query.tanstack.com/_next/static/images/logo-7a7896631260eebffcb031765854375b.svg)

# Overview

React Query는 종종 React에 대한 누락된 데이터의 fetch 라이브러리로 설명되지만 보다 기술적인 용어로 말하면 React 애플리케이션에서 **fetch, 캐싱, 서버 상태 동기화 및 업데이트**를 쉽게 만듭니다.

## 동기부여

기본적으로 React 애플리케이션에는 구성 요소에서 데이터를 가져오거나 업데이트하는 독창적인 방법이 **제공되지 않으므로** 개발자는 결국 데이터를 가져오는 고유한 방법을 구축하게 됩니다. 이는 일반적으로 React 후크를 사용하여 구성 요소 기반 상태와 효과를 함께 꼬집거나 더 범용 상태 관리 라이브러리를 사용하여 앱 전체에 비동기 데이터를 저장하고 제공하는 것을 의미합니다.

대부분의 기존 상태 관리 라이브러리는 클라이언트 상태 작업에 적합하지만 **비동기 또는 서버 상태 작업에는 그다지 적합하지 않습니다**. **서버 상태가 완전히 다르기 때문입니다**. 우선 서버 상태:

- 제어하거나 소유하지 않는 위치에 원격으로 유지됨
- fetch 및 업데이트를 위한 비동기 API 필요
- 공유 소유권을 의미하며 사용자 모르게 다른 사람이 변경할 수 있음
- 주의하지 않으면 애플리케이션이 잠재적으로 "오래된" 상태가 될 수 있음

애플리케이션에서 서버 상태의 특성을 파악하면 진행하면서 **더 많은 문제가 발생**합니다. 예를 들면:

- 캐싱... (아마도 프로그래밍에서 가장 어려운 일)
- 동일한 데이터에 대한 여러 요청을 단일 요청으로 중복 제거
- 백그라운드에서 "오래된" 데이터 업데이트
- 데이터가 "오래된" 경우 파악
- 데이터 업데이트를 최대한 빨리 반영
- 페이지 pagination 및 지연 로딩 데이터와 같은 성능 최적화
- 서버 상태의 메모리 및 garbage 수집 관리
- 구조적 공유를 통한 쿼리 결과 Memoizing

그 목록에 압도되지 않는다면 그것은 아마도 당신이 이미 모든 서버 상태 문제를 해결했고 상을 받을 자격이 있음을 의미해야 합니다. 그러나 대다수의 사람들과 같다면 아직 이러한 문제의 전부 또는 대부분을 해결하지 못했거나 표면만 긁고 있을 뿐입니다!

React Query는 서버 상태를 관리하기 위한 최고의 라이브러리 중 하나입니다. **설정 없이 즉시 사용 가능**하고 놀라울 정도로 잘 작동하며 애플리케이션이 성장함에 따라 **원하는 대로 사용자 custom**할 수 있습니다.

React Query를 사용하면 서버 상태의 까다로운 문제와 장애물을 극복하고 극복하고 앱 데이터가 제어를 시작하기 전에 앱 데이터를 제어할 수 있습니다.

좀 더 기술적인 부분에서 React Query는 다음과 같은 기능을 할 것입니다:

- 애플리케이션에서 복잡하고 오해의 소지가 있는 **여러 줄**의 코드를 제거하고 몇 줄의 React Query 로직으로 대체할 수 있도록 도와줍니다.
- 새로운 서버 상태 데이터 소스 연결에 대한 걱정 없이 애플리케이션을 유지 관리하기 쉽고 새로운 기능을 더 쉽게 구축할 수 있습니다.
- 애플리케이션을 그 어느 때보다 빠르고 반응성이 좋게 만들어 최종 사용자에게 직접적인 영향을 줍니다.
- 잠재적으로 대역폭을 절약하고 메모리 성능을 높이는 데 도움이 됩니다.

## 충분한 이야기를 했으니 준비된 코드를 보여주세요!

아래 예에서 가장 기본적이고 간단한 형태의 React Query가 React Query GitHub 프로젝트 자체에 대한 GitHub 통계를 가져오는 데 사용되는 것을 볼 수 있습니다:

[CodeSandBox 로 보기](https://codesandbox.io/s/github/tannerlinsley/react-query/tree/master/examples/simple)

```js
import { QueryClient, QueryClientProvider, useQuery } from "react-query";

const queryClient = new QueryClient();

export default function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <Example />
    </QueryClientProvider>
  );
}

function Example() {
  const { isLoading, error, data } = useQuery("repoData", () =>
    fetch("https://api.github.com/repos/tannerlinsley/react-query").then(
      (res) => res.json()
    )
  );

  if (isLoading) return "Loading...";

  if (error) return "An error has occurred: " + error.message;

  return (
    <div>
      <h1>{data.name}</h1>
      <p>{data.description}</p>
      <strong>👀 {data.subscribers_count}</strong>{" "}
      <strong>✨ {data.stargazers_count}</strong>{" "}
      <strong>🍴 {data.forks_count}</strong>
    </div>
  );
}
```

_last update : 2022.01.04_
