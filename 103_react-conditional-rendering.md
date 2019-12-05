## 조건부 렌더링

특정 조건이 참인지 거짓인지에 따라 다른 결과를 보여준다.

```
<Hello name="react" isSpecial={true}>
{/*-> 이렇게 줄일 수 있다.*/}
<Hello name="react" isSpecial>

---------------------------------------

<div>
	{isSpecial ? <b>*</b> : null}
	{/*-> 이렇게 변경할 수 있다. */}
	{isSpecial && <b>*</b>}
</div>
```

< Hello isSpecial > isSpecial이 전달해주는 boolean값에 따라 

react에서 undifiend, null, false과같이 나타나지 않는 값은 없는 값으로 취급한다.  furthy한 값은 나타나지 않지만 0은 예외이다.