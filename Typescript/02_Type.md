> Typescript라는 이름 그대로 사용할 변수의 형태를 지정할 수 있음

### Type 지정 방법
- 사용할 변수 옆에 콜론(:)과 지정할 타입을 입력
- 명시적으로 타입을 입력하지 않더라도 변수 선언과 동시에 초기화하면 Typescript가 자동으로 타입을 추론함
	```Typescript
	let specifiedType: string = "This is a string type"
	let unspecifiedType = "This is a string type too, but not recommended."
	```
