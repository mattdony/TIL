> CSS의 display 속성의 `inline`, `block`, `inline-block` 에 대한 사전지식이 있을 경우 이해가 수월할 수 있음
### Flexbox를 사용하는 이유
- 레이아웃을 구성하는데 있어 flexbox를 사용하지 않고 요소들을 특정 위치에 배치하기 위해선, 각각의 요소에 대해 브라우저의 크기를 고려해 위치값들을 직접 계산해서 입력해줘야 하며, 브라우저의 크기가 바뀔 때마다 새롭게 계산하고 수정해줘야 한다.
- Flexbox는 레이아웃을 구성하는 요소들 각각에 하나하나 값을 지정하는 방식인 **명령형**의 불편함을 해소하기 위해, **선언형**으로 요소들이 위치해야할 곳을 기술함으로서 요소들의 위치 값을 브라우저가 크기에 따라 동적으로 계산한다.

<br>

### Flexbox의 사용하기
1. 일반적으로 표현할 요소의 부모요소에 표현방식을 선언한다. 
	```css
	/* style.css */
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
	<!-- index.html -->
	<head>
		<link rel="stylesheet" href="style.css" />
	</head>

	<body>
		<div class="parents">
			<div class="child"></div>
			<div class="child"></div>
			<div class="child"></div>
		</div>
	</body>
	```

<br>

### flex-direction
> - [*] Flexbox의 축(axis) 개념 (매우 중요한 개념 반드시 암기)
> - 
- Flexbox에는 주축(main axis)과 교차축(cross axis) 두 가지 축이 있으며, 축의 방향에 따라 요소들이 배치된다.

- **주축(Main Axis)**
	- `flex-direction` 으로 **주축의 방향을 설정**할 수 있으며 기본값은 `row` 이다.
		```css
		.parents {
			display: flex;
			/* flex-direction: row; 기본값 */
		}
		```
	- `flex-direction` 값에 따라 주축은 네 가지 방향을 갖는다.
		- `row`: ➡️ (왼쪽 > 오른쪽)
		- `row-reverse`: ⬅️ (오른쪽 > 왼쪽)
		- `column`: ⬇️ (위 > 아래)
		- `column-reverse`: ⬆️ (아래 > 위)
	- `justify-conetnt` 속성을 통해 주축방향으로 요소들이 어떻게 배치될 것인지 설정 할 수 있다.

- **교차축(Cross Axis)**
	- 주축과 수직을 이루며 `flex-direction` 을 통해 주축을 설정하면 수직방향으로 별도의 선언 없이 자동으로 교차축이 설정된다.
	- `flex-direction` 에 따라 교차축은 두 가지 방향을 갖는다.
		- `row`, `row-reverse` : ⬇️ (위 > 아래)
		- `column`, `column-reverse`: ➡️ (왼쪽 > 오른쪽)
	- `align-items` 속성을 통해 교차축방향으로 요소들이 어떻게 배치될 것인지 설정 할 수 있다.
- 예시
	```css
	/* sytle.css */
	.parents {
		height: 300px;
		display: flex;
		flex-direction: row-reverse;
		justify-content: space-around;
		align-items: center;
	}
	
	.child {
		width: 100px;
		height: 100px;
		background-color: purple;

		/* 숫자를 가운데 표시하기 위한 속성 */
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 50px;
		color: whitesmoke;
	}
	```

	```html
	<!-- index.html -->
	<div class="parents">
		<div class="child">1</div>
		<div class="child">2</div>
		<div class="child">3</div>
		<div class="child">4</div>
	</div>
	```
	
	![[CSS Layout Masterclass/assets/fig01.png]]

<br>

### flex-wrap
> - Flexbox 안의 자식요소들에 대해 다중라인 여부를 결정
- **한 줄로 표시(Single Line)**
	- `flex-wrap`의 기본값은 `nowrap` 으로, 자식 요소들을 한줄로 표현한다.
	- 자식 요소들의 총 넓이(width)가 부모인 flexbox의 넓이보다 큰 경우, 자식요소의 넓이가 축소된다.
	- 예시
		```css
		/* sytle.css */
		.parents {
			display: flex;
			/* flex-wrap: nowrap; 기본값*/
			gap: 10px;
		}
		
		.child {
			width: 100px;
			height: 100px;
			background-color: purple;
	
			/* 숫자를 가운데 표시하기 위한 속성 */
			display: flex;
			justify-content: center;
			align-items: center;
			font-size: 50px;
			color: whitesmoke;
		}
		```

		```html
		<!-- index.html -->
		<div class="parents">
			<div class="child">1</div>
			<div class="child">2</div>
			...
			<div class="child">14</div>
			<div class="child">15</div>
		</div>
		```
		
		![[CSS Layout Masterclass/assets/fig02.png]]

- **여러 줄로 표시(Multi Line)**
	- `felx-wrap`의 속성을 `wrap`으로 할 경우 자식 요소들의 길이에 맞춰 여러줄로 나타낸다.
	- 예시
		```css
		/* sytle.css */
		.parents {
			display: flex;
			felx-wrap: wrap;
			gap: 10px;
		}
		```

		```html
		<!-- index.html -->
		<div class="parents">
			<div class="child">1</div>
			<div class="child">2</div>
			...
			<div class="child">14</div>
			<div class="child">15</div>
		</div>
		```
		
		![[CSS Layout Masterclass/assets/fig03.png]]
	- `wrap-reverse`의 경우 마지막줄부터 표시된다.
		![[CSS Layout Masterclass/assets/fig04.png]]

<br>

### align-content
> - Flexbox로 자식요소를 여러줄로 나타낼때 자식 요소들 간의 배치 형태를 결정
- `align-content`는 자식요소가 여러줄일 경우에만 동작한다.
- `align-content`는 교차축을 기준으로 자식 요소들을 배치하며, 주축을 기준으로 자식 요소를 배치하는 `justify-content`의 유사하다.
- align-items 와 align-content 비교 예시
	- `align-items: flex-end` vs `align-content: flex-end`
	![[CSS Layout Masterclass/assets/fig05.png]]
	- 양쪽 모두 `flex-direction: row;`이며, 같은 `height`와 `gap` 을 적용
	- `align-items`의 경우 자식요소 전체를 교차축의 끝방향으로 배치시키지만, `height`값을 줄간격을 자동으로 계산해 지정한 `gap` 보다 더 많이 벌어진다. (부모 flexbox의 높이 값이 클수록 줄 간격도 커진다.)
	- `align-content`의 경우 지정한 `gap`을 유지하며 자식 요소 전체를 교차축의 끝방향으로 배치시킨다. (부모 flexbox의 높이 값에 상관없이 자식요소들의 줄간격이 유지된다.)

<br>

### flex-flow
> - `flex-direction` 과 `flex-wrap` 을 한번에 사용할 수 있는 속성
- `flex-direction` 속성의 값(`row`, `row-reverse`, `column`, `column-reverse`)과 `flex-wrap` 속성의 값(`nowrap`, `wrap`, `wrap-reverse`)들을 모두 사용할 수 있다.
- `flex-direction`과 `flex-wrap`의 속성 중 하나 또는 두 속성을 한번에 정해줄 수 있다. (속성 값의 순서는 상관없음)
- 예시
	```css
	/* style.css */
	.parents {
		/* flex-direction: column; 과 같은 기능*/
		flex-flox: column;
	}
	```

	```css
	/* style.css */
	.parents {
		/* flex-direction: column; */
		/* flex-wrap: wrap; */
		
		/* 위의 두 줄과 같은 기능 */
		flex-flox: column wrap;
	}
	```
