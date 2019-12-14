### 설치

#### react router

자체적인 상태는 없이 주소에 대해서 랜더링해줘요라고 정의만 내림

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

#### api 주소 접근

```
/watch/:id                   //rest api 데이터 전달법
/watch?v=saqfsdf             //queryString 전달
```

1. :다음에 임의의 id를 쓸 수 있다. 
2. ?v=sasfsaf // 변수를 여러개를 보낼 수 있다. 공유하기나 그런 옵션들은 많이 들어간다. 이것들까지 사용하는 방법

#### queryString

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

**history.push(/주소)**  
브라우저의 history에다가 url을 변경 된것 처럼 보여주는 작업.

```
props.history.push(`주소`); //setState가 아니라 브라우저 history에 메소드를 사용해서 url 변경
```

로컬 스토리지 : 클라이언트에 데이터 저장, 많이 쓰이는 방법은 아님

-결론: app.js 클릭했을때 setState를 해주는게 아니라 브라우저 history.push 메소드를 사용해서 URL을 변경시키는 요청을 한다. 해당하는 컴포넌트가 독립적인 컴포넌트가 됬으므로 상위 컴포넌트에서 받을 필요 없이 url만 파싱하면된다.  파싱하는 방법이 Route path에서 정의된 변수들을 사용하면 되고 이 변수들은 이 라우트라는 컴포넌트를 쓸 때에만 리엑트 라우터가 동적으로 props라는 객체 안에 매치에 params로 객체로 정의되어있기 때문에 비구조화를 이용해서 사용할 수 있다.

 -라우터에 일치하는 component가 랜더링 됨. 경로와 컴포넌트만 매칭하면 되고, 페이지에 맞는 독립적인 컴포넌트로 분리할 수 있음.



#### SPA

페이지는 싱글이다. 다른 페이지로 전환되지 않음. 사용자로 하여금 주소 이동,  공유도 해야함. 