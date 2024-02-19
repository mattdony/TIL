> CSS의 display 속성의 `inline`, `block`, `inline-block` 에 대한 사전지식이 있을 경우 이해가 수월할 수 있음
### Flexbox를 사용하는 이유
- 레이아웃을 구성하는데 있어 flexbox를 사용하지 않고 요소들을 특정 위치에 배치하기 위해선, 각각의 요소에 대해 브라우저의 크기를 고려해 위치값들을 직접 계산해서 입력해줘야 하며, 브라우저의 크기가 바뀔 때마다 새롭게 계산하고 수정해줘야 한다.
- Flexbox는 레이아웃을 구성하는 요소들 각각에 하나하나 값을 지정하는 방식인 **명령형**의 불편함을 해소하기 위해, **선언형**으로 요소들이 위치해야할 곳을 기술함으로서 요소들의 위치 값을 브라우저가 크기에 따라 동적으로 계산한다.

### Flexbox의 사용하기
1. 일반적으로 표현할 요소의 부모요소에 표현방식을 선언한다. 
	```css
	/* CSS */
	.parents {
		display: flex; /* flexbox 설정 */
		gap: 10px; /* 자식요소들 간의 간격을 부모요소에 설정*/
	}

	.child {
		width: 100px;
		height: 100px;
		background-color: orange;
	}
	```
	
	```html
	<!-- HTML -->
	<div class="parents">
	  <div class="child"></div>
	  <div class="child"></div>
	  <div class="child"></div>
	</div>
	```

### Flexbox의 축(axis)의 개념
- Flexbox에는 주축(main axis)과 교차축(cross axis) 두 가지 축이 있다.
- 
