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
2. Swtich: Switch문과 쓰임세가 같다. 하위에 라우터 중 하나를 선택한다
3. Route :  요청 경로를 다른 경로로 리다이렉션한다
4. Route.props :   history, location, match
   - location.search:  query - string을 반환 
   - match.params: /:요소 를 객체 형태로 반환



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



### HOC - high order component

하이오더컴포넌트. 고차 컴포넌트는 컴포넌트 로직을 재사용하기 위한 React의 고급 기술. 고차 컴포넌트는 컴포넌트를 취하여 새로운 컴포넌트를 반환하는 함수이다.

