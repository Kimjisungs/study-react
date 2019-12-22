## Flow Code

### App.js

```react
import React from 'react';
import { Combine } from './duks'
import CounterRender from './duks'
import { Provider } from 'react-redux';
import { createStore } from 'redux';

const App = () => {
  return (
    <div>
      <Provider store={createStore(Combine)}>
        <CounterRender />
      </Provider>
    </div>
  )
}

export default App;
```

1. Provider : react-redux의 컴포넌트, redux통장을 만들어 주는 역할을 한다.
2. CreateStore(reducer): Redux의 저장소를 만들어준다.
3. reducer: redux저장소에 올라갈 순수함수의 return된 값이 저장된다.

### duks.js

```react
import React from 'react';
import { combineReducers, bindActionCreators } from 'redux';
import { connect } from 'react-redux'

const PLUS = 'PLUS';
const MINUS = 'MINUS';

const plus = value => ({ type: PLUS, value})
const minus = value => ({ type: MINUS, value})

const INITIAL_STATE = {
  count: 0
}

const counter = (state=INITIAL_STATE, action) => {
  switch(action.type) {
    case PLUS:
      return {
        ...state,
        count: state.count + action.value
      }
    case MINUS:
      return {
        ...state,
        count: state.count - action.value
      }
    default:
      return state
  }
}

export const Combine = combineReducers({
  counter,
})


const CounterRender = props => {
  return (
    <div>
      {console.log(props)}
      <button type="button" onClick={()=> props.plus(1)}>더하기</button>
      <span className="count">
        {
          props.count
        }
      </span>
      <button type="button" onClick={()=> props.minus(1)}>빼기</button>
    </div>
  )
}

const mapStateToProps = state => ({ count: state.counter.count })

const mapDispatchToProps = dispatch => bindActionCreators({
  plus,
  minus,
}, dispatch)

export default connect(mapStateToProps, mapDispatchToProps)(CounterRender)
```

1. Action: dispatch에 의해 정의 된 함수가 실행되면 실행된 { type } 타입이 reducer에 전달되며,

2. reducer: reducer가 type을 체크하여 순수함수로 계산 후 store에 전달한다.

   