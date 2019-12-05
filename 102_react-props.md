## props - properties

컴포넌트에게 값 전달하기 props의 파라미터는 넘겨준 것들이 객체 형태로 반환

**hello.js**  

```react
import React from 'react';

function Hello({ color, name }) {
  return <div style={{ color }}>안녕하세요 {name}</div>
}

Hello.defaultProps = {
  name: '이름없음'
}

export default Hello;
```



**Wrapper.js**

```javascript
import React from 'react';

function Wrapper( { children } ) {
  const style = {
    border: '2px solid black',
    padding: 16
  };

  return <div style={style}>{children}</div>
}

export default Wrapper;
```



**App.js**

```react
import React from 'react';
import Hello from './Hello';
import Wrapper from './Wrapper';


function App() {
  return (
    <Wrapper>
      <Hello name="react" color="red" />
      <Hello color="blue" />
    </Wrapper>
  )
}
```



### prors 속성

type, props, child가 있다. 

#### props - props 전달

```
<Hello name="react" color="red">

------------------------------------------

const Hello = ({ color, name }) => <div style={{ color }}>안녕하세요 {name}</div>

export default Hello;
```

< Hello name="react" color="red" >의 name="react", color="red"는 props파라미터에 의해 객체 형태로 전달된다. 

component로 사용될 const Hello 함수는 import React 의 props의 값으로 color, name을 매개변수로 전달 받고, 실제로 보여지게될 jsx의 태그에 전달받은 매개변수로 데이터를 적용하여 component와 같이 사용할 수 있다.

#### props가 전달되지 않을때 default 값

```
Hello.defaultProps = {
  name: '이름없음'
}
```

< Hello >는 함수 실행문에 props속성을 넘기지 않으면 기본값으로 정의되는 값이다. 

#### props - children

```
import React from 'react';
import Hello from './Hello';
import Wrapper from '.Wrapper';

<Wrapper>
    <Hello name="react" color="red" />
    <Hello color="blue" />
</Wrapper>

----------------------------------------------

import React from 'react';

const Wrapper = ( { children } ) => {
  const style = {
    border: '2px solid black',
    padding: 16
  };

  return <div style={style}>{children}</div>
}
```

< wrapper > 함수가 실행되어 리턴된 값을 전달받고   
import Wrapper from '.Wrapper'; 로부터

{ children } 은 props의 프로퍼티로 length를 가지고있는 유사 배열 객체를 반환하여 표현한다.

