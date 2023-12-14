# Movie App (TypeScript ver.)

OMDb API를 활용해 VanillaJS 영화 검색 애플리케이션을 만들어봅니다.  
이 프로젝트는 [JS 버전](https://github.com/ParkYoungWoong/vanillajs-movie-app/tree/js-only)과 [TS 버전](https://github.com/ParkYoungWoong/vanillajs-movie-app/tree/main)으로 나누어져 있습니다.  
기본 버전은 TS입니다.

[DEMO](https://vanilla-movie-5znvu8s4t-parkyoungwoong.vercel.app/#/) 

![image](https://github.com/mihye0924/movie-app/assets/71968785/290173bd-2ac9-412f-83f9-f1ba31f7062c)

------------------------

### 프로젝트 시작하기

```bash
$ npm i
$ npm run vercel
```

------------------------

### Reset.css

브라우저의 기본 스타일을 초기화합니다.

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reset-css@5.0.1/reset.min.css" />
```

------------------------

### Google Fonts

[Oswald](https://fonts.google.com/specimen/Oswald?query=oswa), [Roboto](https://fonts.google.com/specimen/Roboto?query=robo) 폰트를 사용합니다.

```html
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@500&family=Roboto:wght@400;700&display=swap" rel="stylesheet" />
```

------------------------

### Headline.js HTML 

```html
<h1>
  <span>OMDb API</span><br />
  THE OPEN<br />
  MOVIES DATABASE
</h1>
<p>
  The OMDb API is a RESTful web service to obtain movie information,
  all content and images on the site are contributed and maintained by our users.<br />
  If you find this service useful, please consider making a one-time donation or become a patron.
</p>
```

------------------------

## Vercel Hosting

`node-fetch` 패키지는 꼭 2버전으로 설치해야 합니다!

```bash
$ npm i -D vercel dotenv
$ npm i node-fetch@2
```

__/vercel.json__

```json
{
  "devCommand": "npm run dev",
  "buildCommand": "npm run build"
}
```

__/package.json__

```json
{
  "scripts": {
    "vercel": "vercel dev"
  }
}
```

------------------------

### Vercel 개발 서버 실행

Vercel 구성 이후에는 `npm run dev`가 아닌 `npm run vercel`로 개발 서버를 실행해야 합니다!

```bash
$ npm run vercel
```

------------------------

## Vercel Serverless Functions

프로젝트 루트 경로에 `/api` 폴더를 생성하고,   
API Key 를 노출하지 않도록 서버리스 함수를 작성합니다.

__/api/movie.js__

```js
import fetch from 'node-fetch'

const { APIKEY } = process.env

export default async function handler(request, response) {
  const { title, page, id } = JSON.parse(request.body)
  const url = id
    ? `https://www.omdbapi.com/?apikey=${APIKEY}&i=${id}&plot=full`
    : `https://www.omdbapi.com/?apikey=${APIKEY}&s=${title}&page=${page}`
  const res = await fetch(url)
  const json = await res.json()
  response
    .status(200)
    .json(json)
}
```

------------------------

### 환경변수

로컬의 개발용 서버에서 사용할 환경변수를 `.env` 파일에 지정합니다.

__/.env__

```dotenv
APIKEY=<MY_OMDb_API_KEY>
```

제품 서버(Vercel 서비스)에서 사용할 환경변수를 지정합니다.  
Vercel 서비스의 프로젝트 __'Settings / Environment Variables'__ 옵션에서 다음과 같이 환경변수를 지정합니다.
 

------------
## Stacks

#### Environment   
<img src="https://github.com/mihye0924/react_context_app/assets/71968785/6e825b86-c259-48c2-a272-4286e74d9798" width="30">
<img src="https://github.com/mihye0924/react_context_app/assets/71968785/557f00bf-2f5f-4bc9-9d63-10565250d6f9" width="30">
<img src="https://github.com/mihye0924/react_context_app/assets/71968785/64f67e8b-759f-4063-a3bc-29dc3918e44b" width="30">

#### Config
<img src="https://github.com/mihye0924/react_context_app/assets/71968785/64725c2b-af8d-4891-9ef1-f1068d1fd019" width="30">

#### Development
<img src="https://github.com/mihye0924/react_context_app/assets/71968785/d9784930-b259-4f5f-a941-568068f1d73d" width="30">  
<img src="https://github.com/mihye0924/movie-app/assets/71968785/3268ef6d-a93e-4c32-beee-614e57e0712a" width="30">
<img src="https://github.com/mihye0924/PERIPERA/assets/71968785/f71d27fe-0839-43c4-bafe-7f9fe7474639" width="30">

 
#### Deploy 
<img src="https://github.com/mihye0924/lotto_6_deploy/assets/71968785/085a4946-cf48-4255-a185-1fc68851795e" width="30">

