![Next.js](https://upload.wikimedia.org/wikipedia/commons/8/8e/Nextjs-logo.svg)

# Getting Started

Next.js 문서에 오신 것을 환영합니다!

Next.js가 처음이라면 [학습 과정](https://nextjs.org/learn/basics/create-nextjs-app)부터 시작하는 것이 좋습니다.

퀴즈가 포함된 대화형 과정은 Next.js를 사용하기 위해 알아야 할 모든 것을 안내합니다.

Next.js와 관련된 질문이 있으면 언제든지 [GitHub Discussions](https://github.com/vercel/next.js/discussions)에서 커뮤니티에 질문할 수 있습니다.

### System Requirements

- 최소 [Node.js 12.22.0](https://nodejs.org/en/) 버전
- MacOS, Windows(WSL 포함) 및 Linux 지원

## 설정

모든 것을 자동으로 설정하는 `create-next-app`을 사용하여 새로운 Next.js 앱을 만드는 것이 좋습니다. 프로젝트를 만들려면 다음을 실행하세요:

```
npx create-next-app@latest
# 또는
yarn create next-app
```

TypeScript 프로젝트로 시작하려면 --typescript 플래그를 사용할 수 있습니다:

```
npx create-next-app@latest --typescript
# 또는
yarn create next-app --typescript
```

설치가 완료된 후:

- `npm run dev` 또는 `yarn dev`를 실행하여 `http://localhost:3000`에서 개발 서버를 시작합니다.
- 애플리케이션을 보려면 `http://localhost:3000`을 방문하십시오.
- `page/index.js`를 편집하고 브라우저에서 업데이트된 결과를 확인하세요.

`create-next-app` 사용 방법에 대한 자세한 내용은 [`create-next-app` 설명서](https://nextjs.org/docs/api-reference/create-next-app)를 참조하세요.

## 수동 설정

`next`을 설치하고 프로젝트에 `react` 및 `react-dom`을 설치하십시오.

```
npm install next react react-dom
# 또는
yarn add next react react-dom
```

`package.json`을 열고 다음 `scripts`를 추가합니다:

```
"scripts": {
  "dev": "next dev",
  "build": "next build",
  "start": "next start",
  "lint": "next lint"
}
```

다음 스크립트는 애플리케이션 개발의 여러 단계를 참조합니다:

- `dev` - 개발 모드에서 Next.js를 시작하는 `next dev`을 실행합니다.
- `build` - 프로덕션 사용을 위해 애플리케이션을 빌드하는 `next build`를 실행합니다.
- `start` - Next.js 프로덕션 서버를 시작하는 `next start`을 실행합니다.
- `lint` - Next.js의 내장 ESLint 구성을 설정하는 `next lint`를 실행합니다

Next.js는 [pages](https://github.com/qudwnbj/qudwnbj-translation-docs-md/blob/master/Next.js/Basic%20Features/pages.md) 개념을 중심으로 구축되었습니다. 페이지는 `pages` 폴더의 `.js`, `.jsx`, `.ts` 또는 `.tsx` 파일에서 내보낸 [React Component](https://reactjs.org/docs/components-and-props.html)입니다.

페이지는 파일 이름에 따라 경로와 연결됩니다. 예를 들어 `pages/about.js`는 `/about`에 매핑됩니다. 파일 이름으로 동적 경로 변수를 추가할 수도 있습니다.

프로젝트 내부에 `pages` 폴더를 만듭니다.

다음 내용으로 `./pages/index.js`를 채웁니다:

```js
function HomePage() {
  return <div>Welcome to Next.js!</div>;
}

export default HomePage;
```

지금까지 우리는 다음을 얻습니다:

- 자동 컴파일 및 번들링(webpack 및 babel 포함)
- [React 빠른 새로 고침](https://nextjs.org/blog/next-9-4#fast-refresh)
- [`./pages/`](https://github.com/qudwnbj/qudwnbj-translation-docs-md/blob/master/Next.js/Basic%20Features/pages.md)의 [static generation 및 server-side rendering](https://github.com/qudwnbj/qudwnbj-translation-docs-md/blob/master/Next.js/Basic%20Features/data-fetching.md)
- [정적 파일 제공](https://github.com/qudwnbj/qudwnbj-translation-docs-md/blob/master/Next.js/Basic%20Features/static-file-serving.md). `./public/`은 `/`에 매핑됩니다.

또한 모든 Next.js 애플리케이션은 처음부터 프로덕션에 사용할 준비가 되어 있습니다. 자세한 내용은 [배포 문서](https://nextjs.org/docs/deployment)를 참조하세요.

_last update : 2022.01.04_
