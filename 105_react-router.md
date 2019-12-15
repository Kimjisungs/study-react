### react router

```
npm i react-router //react router 설치

import { 
	BrowserRouter as Router,
	Switch,
	Route
} from "react-router-dom"; //react router dom은 리엑트 라우터를 설치하면 자동 사용 가능
```

```
<Router>
	<Switch>
		<Route path="/watch/:id" component={ videoPlayer }>
		<Route path="/watch" component={ videoPlayer }>
		<Route path="/results" component={ Main }>
		<Route path="/" component={ Main }>
	</Swtich>
</Router>
```



1. Router: 가장 기본적인것, 라우터 컴포넌트 안에서 어떠한 주소에 대해서 해당 컴포넌트를 사용하겠다. 시작과 끝에서 사용할 수 있음. 집합
2. Swtich: es5와 같은 맥락, 
3. Route: path값을 정확하게 하려면 exact를 적어줘야 한다. 실제 경로 지정해서 컴포넌트를 연결 해 준다. 
4. path: 실제 주소, queryString을 정의하지 않는다. queryString은 클라이언트 요청시 덫붙혀서 보낸다.  path의 url 순서가 중요한데, path의 url은 앞쪽이 맞으면 반환하기 때문에 뒤의 url을 가고싶어도 뒤의 url이 앞쪽과 똑같이 시작한다면 접근조차 되지 않아 exact를 써 주거나 위로 올린다.
5. component: path에 접근하는 해당 컴포넌트를 맵핑만 하면 된다. Route라는 컴포넌트가 props를 동적으로 넣어준다. url기준으로  

-- react router 안의 route 컴포넌트가 props를 path를 감지하여 그 component를 컴포넌트 props값의 컴포넌트에 전달한다.

### api 주소 접근 방법

```
/watch/:id                   //rest api 데이터 전달법
/watch?v=saqfsdf             //queryString 전달
```

1. :다음에 임의의 id를 쓸 수 있다. 
2. ?v=sasfsaf // 변수를 여러개를 보낼 수 있다. 공유하기나 그런 옵션들은 많이 들어간다. 이것들까지 사용하는 방법

### queryString

```
npm install query-string
// 참고 url https://www.npmjs.com/package/query-string

import qs from 'query-string';

const { id } = props.match.params; 

const { v } = qs.parse(props.location.search)

const url = `https://youtube.com/embed/${id || v}`
```

1. **rest api  와 같은 주소의 경우**  

   const { id } = props.match.params // react router path에 아이디 정의

   match가 되는 파라미터를 가지고 와라.

2. **queryString과 같이 사용될때**  
   -react router에서 정의되어있는객체 qs.parse(props.location.search)    
   qs.parse는 그 다음에 나오는 queryString을 파싱해준다.

#### history.push(), history,GoBack()

하이퍼링크 타고 페이지가 바뀌는게 아니라 주소만 바뀌는것.

**특징** : 콘솔 로그가 그대로 남아있고, 페이지가 refresh되지 않는다.



### history.push(/주소)

 브라우저의 history에다가 url을 변경 된것 처럼 보여주는 작업.

window.location 하이퍼링크와는 다름. 주소가 바뀌는것 처럼 보이나 브라우저 히스토리만 추가해서 그리고 back버튼도 사용할 수 있다. 브라우저에 기록만 남기고 주소를 바뀌는것 처럼 보이게 하고 히스토리가 있다라는 것은 뒤로가기 버튼을 사용할 수 있는 효과가 있다.

```
props.history.push(`주소`); //setState가 아니라 브라우저 history에 메소드를 사용해서 url 변경

props.history.GoBack() 뒤로가기
```

#### Route의 컴포넌트의 기본적인 props match, history, location

**history, match, location**

전달 방법 -> route path에게

- props.history.push는 react-router-dom 에 정의되어있는   
  { withRouter } 함수를 사용해야한다. history.push는 리엑트 자체에 정의되어 있지않기 때문에 이걸 사용하는 방법은  

  ```
  export default widthRouter(App);
  
  //history.push는 리엑트에 정의되어있지 않고 리엑트 라우터 돔에 정의되어있다. App를 인자로 받아서 실행해서 모듈로 넘김
  ```



### withRouter

```
import { withRouter } from 'react-router-dom';

export default widthRouter(Main)
```

withRouter 함수에 실행될 함수 인자를 넘겨주어야 react component에 정의되어있지 않은 props의 history와 같은 react component에 정의되어 있지 않은 컴포넌트를 사용할 수 있다. withRouter함수가 이때 실행될 함수를 인자로 넘기고 props도 전달한다.



로컬 스토리지 : 클라이언트에 데이터 저장, 많이 쓰이는 방법은 아님

-결론: app.js 클릭했을때 setState를 해주는게 아니라 브라우저 history.push 메소드를 사용해서 URL을 변경시키는 요청을 한다. 해당하는 컴포넌트가 독립적인 컴포넌트가 됬으므로 상위 컴포넌트에서 받을 필요 없이 url만 파싱하면된다.  파싱하는 방법이 Route path에서 정의된 변수들을 사용하면 되고 이 변수들은 이 라우트라는 컴포넌트를 쓸 때에만 리엑트 라우터가 동적으로 props라는 객체 안에 매치에 params로 객체로 정의되어있기 때문에 비구조화를 이용해서 사용할 수 있다.

 -라우터에 일치하는 component가 랜더링 됨. 경로와 컴포넌트만 매칭하면 되고, 페이지에 맞는 독립적인 컴포넌트로 분리할 수 있음.

-URL이 바뀌는 시점에 Router가 작동한다.

#### SPA

페이지는 싱글이다. 다른 페이지로 전환되지 않음. 사용자로 하여금 주소 이동,  공유도 해야함. 

### .env

환경변수

~~~
.env 파일

REACT_APP_YOUTUBE_API_KEY=나의

   const params = {
      key: process.env.REACT_APP_YOUTUBE_API_KEY,
      q: query,
      part: `snippet`,
      maxResults: 4,
    }

~~~

