1. ### App.js

   ```react
   import { Provider } from 'react-redux';
   import { createStore } from 'redux';
   import reducers from './reducers'
   
   const App = () => (
     <Provider store={createStore(reducers)}>
       <Router>
         <Switch>
           <Route path="/watch/:id" component={VideoPlayer} />
           <Route path="/watch" component={VideoPlayer} />
           <Route path="/results" component={Main} />
           <Route path="/" component={Main} />
         </Switch>
       </Router>
     </Provider>
   )
   export default App;
   ```

   1. Provider : react-redux의 전체 앱의 컴포넌트 트리가 포함 된 최상위 레벨에서 랜더링. createStore 상점을 만드는것처럼, redux에 통장을 생성.
   2. createStore(reducer) : 앱의 완전한 상태 트리를 보유하는 Redux 저장소를 만든다.
   3. reducer : 현재 상태 트리와 처리 할 동작이 주어지면 다음 상태 트리를 반환하는 축소 함수 이다.

   

   ### reducers/index.js 상점 생성에 update할 저장소 모임 파일 생성

   ```react
   import { combineReducers } from 'redux';
   
   import counter from './counter';
   
   export default combineReducers({
   	counter,
   	videos,
   	etc,
   })
   ```

   1. combineReducers 헬퍼 함수는 서로 다른 리듀싱 함수들을 값으로 가지는 객체를 받아서 createStore에 넘길 수 있는 하나의 리듀싱 함수로 바꿔준다. combineReducers는 결과를 모아서 하나의 상태 객체 로 바꿔주는데 이때 상태 객체의 형태는 reducers로 전달된 키들을 따른다.

   

   ### actions/index.js

   ```react
   export const Add = "ADD"  //무조건 스트링
   
   export function add(val) {
       return ({ type: ADD, val })
   }
   ```

   1. action: 상점으로 데이터 정보를 보내는 페이로드이다.
   2. actions creators : action을 리턴해 주는 함수. 여러가지 값이 올 수 있다. 

   

   ### reducers/counter.js 리듀서 파일 생성

   ```react
   import { ADD } from '../actions'
   
   const INITIAL_STATE = {
       count: 0,
   }
   
   export default function counter(state=INITIAL_STATE, action) {
       switch(action.type) {
           case ADD: 
               return {
                   ...state,
                   count: state.count + action.val
               }
           default: 
               return state
       }
   }
   ```

   1. counter함수는 reducer함수이다. 
   2. state의 초기값 INITIAL_SATE를 설정하지 않으면 초기 값은 undefined가 된다. undefined일때 초기값을 설정한다.

   

   ```react
   import React from 'react';
   import { connect } from 'react-redux';
   import { bindActionCreators } from 'redux';
   
   import { add } from './actions';
   
   const Counter = props => (
     // store.dispatch({type: ADD, val})
     <div>
       <button type="button" onClick={() => props.add(1)}>+</button>
       {props.count}
       <button type="button" onClick={() => props.add(-1)}>-</button>
     </div>
   )
   
   function mapStateToProps(state) {
     return {
       count: state.counter.count
     }
   }
   
   function mapDispatchToProps(dispatch) {
     return bindActionCreators({
       add,
     }, dispatch)
   }
   
   export default connect(mapStateToProps, mapDispatchToProps)(Counter);
   ```

   

   1. Counter의 props는 단순히 상위 컴포넌트의 props만 전달 받을 수 있기 때문에   
   redux의 state 값을 사용하려면 mapStateToprops(state)와 connect 과정이 필요하다. ? state는 어디로부터 받나.
   2.   mapDispatchToProps: reducer에 전달하는 함수, 
3. mapStateToProps : 
   4. mapDispatchToProps(dispatch) { return bindActionCreators({  add }, dispatch )  } 

   redux component와 state와 dispatch를 따로 전달해 주기 때문에, 얘를 해당하는 컴포넌트에도 쓸 수 있도록, 맵핑 해주는 두가지가 필요한데 mapStateToProps는 redux, reducer가 가지고 있는 변수에 접근하기 위해서 state를 props로 넘겨준다. 
   
   mapDispatchToProps는  원래 dispacth를 써서 action을 전달해야 reducer에 전달 되는데 리엑트에서  복잡하게 하지 않고 props로 전달받은 함수처럼 쓸 수있게 이 함수를 쓴다. 

   bindActionCreators는 action을 리턴해주는 함수다. actionCreators는 여러가지 함수가 있다. 이 함수에서 쓸 함수를 나열해 주면 된다.

   

   
   
   ```
   <Provider store={createStore(reducers)}>
   	<Counter/>
   </Provider>
   
   const Counter = props => (
     <div>
       {console.log(props)}
       <button type="button" onClick={() => props.add(1)}>+</button>
       {props.count}
       <button type="button" onClick={() => props.add(-1)}>-</button>
     </div>
   )
   
   
   ```
   
   
   
   결과 
   
   1. 스토어 생성 및 전체 앱의 컴포넌트 포함 App.js   
      - 이곳에서는 실제 구동 될 counter 컴포넌트를 임포트
   2. reducers/index.js저장소에 reducer를 통합하여 createStore에 넘길 수있는 리듀싱 함수로 바꿔주는 모임 파일 생성.
   3. action/index.js실제 리듀서 파일 생성 actions의 payload값을 export.
   4. reducers/counter.js 페이로드를 reducer함수에서 받아서. 그 함수에서 객체를 가공된 순수 함수의 코드를 덮어씌움.
      - 여기서 state는 기본 state를 적용.    
      - switch문에서 payload를 비교하여 적용.
   5. 실제 구동할 Counter.js