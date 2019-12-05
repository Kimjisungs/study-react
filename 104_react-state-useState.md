## useState - 상태관리 함수형

상태를 관리

```
function App(props) {
  return (
   <Counter />
  )
}

--------------------------------

import React, { useState } from 'react';

function Counter() {
  const [number, setNumber] = useState(0);
  // const numberState = useState(0);
  // const number = numberState[0];
  // const setNumber = numberState[1];

  const onIncrease = () => {
    setNumber(prevNumber => prevNumber + 1);
  }
  const onDecrease = () => {
    setNumber(prevNumber => prevNumber - 1);
  }

  return (
    <div>
      <h1>{number}</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  )
}
```

1. {useState} 를 불러온다.
2. const [number, setNumber] = useState(0);  
   - number = 상태의 기본값은 0으로 하겠다.
   - setNumber = 상태를 변경하겠다.
3. setNumber(number + 1); //이상태를 가져와서 넘버 추가하겠다.  
   -> setNumber(prevNumber => prevNumber + 1 ); // 어떻게 없데이트하겠다 라고 없데이트 함수를 넣어서 표현할 수있다. 리엑트 컴포넌트를 최적화 하기 위해 이렇게 해야한다.