## jsx 문법

~~~javascript
import React from 'react'
~~~



1. class => className

2. img jsx태그에서는 alt를 꼭 써주어야한다.

3. {} 안에는 변수가 들어간다.

4. className, onClick과 같이 두개의 단어가 들어갈때는 camelcase를 사용해야 한다.

5. component를 만든다. 컴포넌트는 항상 대문자로 시작해야 한다.  
   내가 만들때에만 무조건 대문자로 시작해야 한다.  
   ex) const Header < Header >

6. 태그는 꼭 닫혀있어야한다.  
   ex) < div >< /div >, < br / >, < input / >

7. 두개 이상의 태그는 하나의 태그로 감싸져있어야 한다.  

   ~~~javascript
   <div>
   	<Hello />
   </div>
   
   // or fragment
   
   <>
   	<Hello />
   </>
   ~~~

8. 주석 처리방법   

   ~~~javascript
   <>
    {/* 어쩌고 저쩌고 */}
    
    <Hello 
    //이런식으로 주석을 작성
    >
   </>
   ~~~

   

