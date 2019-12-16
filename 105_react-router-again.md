### RouterComponent

```
<BrowserRouter>
basename: string
getUserConfirmation: func
forceRefresh: bool
keyLength: number
children: node

// HTML5 History Api 사용, 브라우저 주소 표시줄의 경로를 바꿔 줄 수 있음. 서버에 요청하지 않고.
```

```
<HashRouter>
basename: string
getUserConfirmation: func
hashType: string
children: node

//주소 뒤에 hash태그삽입. 옛날 브라우저 전용
```

```
<MemoryRouter>
initialEntries:array
initialIndex: number
getUserConfirmation: func
keyLength: number
children: node

//브라우저 주소와는 무관함, 일체 건드리지 않음
//임베디드 웹앱, 리액트 네이티브 등에서 사용
```





## react router

```javascript
import React from 'react';
import {
  BrowserRouter as Router,
  Switch,
  Route
} from "react-router-dom";

const App = () => (
  <Router>
    <Switch>
      <Route path="/watch" component={ VideoPlayer } />
      <Route path="/result" component={ Main } />
      <Route path="/" component={ Main } />
    </Switch>
  </Router>
)

```

1. BrowserRouter as Router : 요청 경로와 렌더링할 컴포넌트를 설정한다. 라우터 컴포넌트 안에서 어떠한 주소에 대해서 해당 컴포넌트를 사용할 수 있음.
2. Swtich: Switch문과 쓰임세가 같다. 하위에 라우터 중 하나를 선택한다. page를 못찾았을때 notFound를 보여줄때 유용.
3. Route :  요청 경로를 다른 경로로 리다이렉션한다
4. Route.props :   history, location, match
   - location.search:  query - string을 반환 
   - match.params: /:요소 를 객체 형태로 반환



### router 부가기능

1. **history**객체  
   -특정 함수를 호출했을때 뒤로가거나 페이지 이탈을 방지할 수 있다.   

   ```
   history.go // 앞혹은 뒤 go(-1)뒤 -2는 두번뒤
   history.goBack() //뒤로가기
   history.length 방문기록 길이
   history.location 자신이 있는 경로 혹은 위치
   history.push() // 특정경로로 이동 방문 기록을 남긴다.
   history.replace() // 방문페이지 기록남기지 않는다. 처음 시작점으로 돌아간다.
   
   history.block() // 사용자 이탈 방지
   ex)
   
   import { useEffect } from 'react'
   useEffect( ()=> {
   	const unblock = history.block('정말 나갈건가요?')
   	return () => {
   		unblock();
   	}
   })
   ```

   

### query-string

```javascript
npm install query-string

import qs from 'query-string';

//http://localhost:3000/result?name=lee
const parsed = qs.parse(location.search)

console.log(location.search) //result?name=lee
console.log(parsed)//{name : lee}
```



### withRouter

react-router-dom 의 Route가 아닌 컴포넌트에서 Route에서 사용하는 객체 - location, match, history를 사용해야 하려면, withRouter라는 HOC를 사용해야 한다.

라우터 컴포넌트가 아닌곳에서사용.

```
import { widthRouter } from 'react-router-dom';

function WithRouterSample({ location, match, history}) {}

export default widthRouter(widthRouterSample);

여기서 location과 match는 
```

-router가사용되지 않는곳에서 조건부로 이동할 때 사용된다.   
route로 사용되지 않은 컴포넌트에서. 로그인이 성공했을때 특정 경로로 가고, 성공하지 않았을때 가만히 있고 싶다.



### NavLink

```
import { NavLink, Route } from 'react-router-dom'


<NavLink
	to="profiles/name"
	activeStyle={{ background:'blue', color: 'white' }}
	activeClassName="active"
	isActive={(match, location) => {
		return match.params = 어쩌고 true false반환해야함
	}}
	ex 경로가 to="/"되어있으면 route컴포넌트와같이 exact를 넣어줘야함
>
	링크
</NavLink>
```

active되었을때 추가 가능



### HOC - high order component

하이오더컴포넌트. 고차 컴포넌트는 컴포넌트 로직을 재사용하기 위한 React의 고급 기술. 고차 컴포넌트는 컴포넌트를 취하여 새로운 컴포넌트를 반환하는 함수이다.

