### useState

```react
import React, { useState } from 'react';

[number, setNumber] = useState(0);

// 바뀌는 값 관리, 상태 업데이트

setNumber(number + 1)  // 
setNumber(prevNumber => prevNumber + 1) // update 함수, 최적화
```

