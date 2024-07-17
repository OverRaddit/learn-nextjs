/app/a/page.tsx 를 생성.

/a url로 접속시 page.tsx 컴포넌트로 연결됨.

경로에 해당하는 폴더를 만들고, 그곳에 page.tsx를 꼭 만들어야 한다.

# layout

자식컴포넌트를 wrapping한다.
여러 페이지 컴포넌트에 고정적으로 들어가는 레이아웃을 담당함.

페이지를 계층구조로 관리한다. 상위계층의 layout은 하위계층에도 적용된다.

상위,하위 모두 레이아웃이 존재할경우 두개가 중첩되어 렌더링된다.

# metadata

상위,하위에서 병합됨. object이므로 key-value쌍으로 값을 등록함.
동일한 key가 있으면 하위에서 등록된게 우선됨. 순서상으로 당연한 거긴함.
메타데이터는 페이지, 레이아웃에서만 등록할 수 있음.

메타데이터의 특정값을 템플릿처럼 만들 수 있다.

# Dynamic Route

/movies/:id와 같은 처리를 할 수 있다.
id와 같은 변수에 해당하는 부분을 "[id]"라는 이름의 폴더로 만들어 둔다.

## prop

페이지 컴포넌트의 prop객체를 보면
params와 searchParams가 있다.
각각 파라미터와 쿼리를 의미한다.

# fetch

서버사이드에서 fetch를 하면 자동으로 url에 대해 캐싱을 진행한다.

> 이 캐싱에 어떻게 구현되어있는 지는 알아볼 필요가 있을 듯.

## loading

fetch가 진행되는 동안 page.tsx처럼 loading.tsx를 만들어 로딩중 보여줄 페이지를 정의할 수 있다.

- react suspense를 내부적으로 사용한다?
  https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming

## 병렬호출

```js
const [movie, videos] = await Promise.all([getMovie(id), getVideos(id)]);
```

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/all

## loading대신 suspense

서버사이드 렌더링인데도,
일부분만 비동기통신을 통해 렌더링가능.

## 왜 error.tsx파일은 use client를 강제해야할까?

에러처리기능이 react기능이고 CSR의 일부라서?
그 논리대로라면 suspense를 쓸때도 마찬가지일텐데...

왜 suspense를 서버컴포넌트에서 쓸수있는거지?
흠~~~
