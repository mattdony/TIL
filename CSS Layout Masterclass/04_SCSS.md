> CSS에 추가기능을 더한 언어이며, 브라우저가 자체적으로 SCSS를 처리할 수 없어 전처리기인 SASS를 통해 SCSS를 CSS로 변환하는 과정을 거친다.

- SCSS를 CSS로 변경하기 위해 [[Vite]], Webpack 등과 같은 도구를 필요로 하며, SASS 전처리기를 추가 해야한다.
	```zsh
	# Vite에서 SASS 전처리기 추가
	npm add -D sass
	```

<br>

### Nesting
- css를 중첩해 중복되는 코드를 줄일 수 있게 해준다.
- 사람의 눈으로 보기에 기존의 css보다 직관적이다.
	```css
	/* style.css */
	body {
		font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
	}

	ul {
		list-style-type: none;
		padding: 0;
		display: flex;
		gap: 10px;
	}


	ul li {
		background-color: tomato;
		color: whitesmoke;
		padding: 5px 10px;
		border-radius: 7px;
	}

	ul li:hover {
		opacity: 0.8;
	}

	ul li a {
		text-decoration: none;
		text-transform: uppercase;
		color: whitesmoke;
	}

	ul li a:hover {
		color: darkslateblue;
	}
	```

	```scss
	// style.scss
	body {
		font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
	}

	ul {
		list-style-type: none;
		padding: 0;
		display: flex;
		gap: 10px;

		li {
			background-color: tomato;
			color: whitesmoke;
			padding: 5px 10px;
			border-radius: 7px;

			&:hover {
				opacity: 0.8;
			}
			
			a {
				text-decoration: none;
				text-transform: uppercase;
				color: whitesmoke;

				&:hover {
					color: darkslateblue;
				}
			}
		}
	}
	```

	```html
	<!-- index.html -->
	<body>
		<ul>
			<li><a href="#">Home</a></li>
			<li><a href="#">About</a></li>
			<li><a href="#">Contact</a></li>
		</ul>
	</body>
	```
	![[CSS Layout Masterclass/assets/scss_fig01.png]]

<br>

### Extend
- 공통된 속성을 정의하고 `@extend`로 상속 받는 것처럼 활용해 코드를 재활용 할 수 있다.
- 정의 또는 사용 시 `%` 기호를 사용한다.
	```scss
	// style.scss
	body {
		font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
	}

	%alert {
		margin: 10px;
		padding: 10px 20px;
		border-radious: 10px;
		border: 1px dashed black;
	}

	%textColor {
		color: whitesmoke;
	}
	
	.success {
		@extend %alert, textColor;
		backgroud-color: green;
	}

	.warning {
		@extend %alert;
		backgroud-color: yellow;
	}

	.error {
		@extend %alert;
		backgroud-color: tomato;
	}
	```

	```html
	<!-- index.html -->
	<body>
		<span class="success">It's all good!</span>
		<span class="warning">Careful!</span>
		<span class="error">On no! Something is wrong!</span>
	</body>
	```
	![[CSS Layout Masterclass/assets/scss_fig02.png]]

<br>

### Mixin
- `@extend`를 사용할 때와 비슷하지만 특정 속성 값에 대해, 사용할때 해당 속성을 결정할 수 있는 argument로 전달 받아 사용한다.
- `@mixin` 으로 선언하고, `@include` 키워드로 사용한다.
	```scss
	// style.scss
	body {
		font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
	}

	@mixin alert {
		margin: 10px;
		padding: 10px 20px;
		border-radious: 10px;
		border: 1px dashed black;
	}
	
	.success {
		@extend %alert, textColor;
		backgroud-color: green;
	}

	.warning {
		@extend %alert;
		backgroud-color: yellow;
	}

	.error {
		@extend %alert;
		backgroud-color: tomato;
	}
	```

	```html
	<!-- index.html -->
	<body>
		<span class="success">It's all good!</span>
		<span class="warning">Careful!</span>
		<span class="error">On no! Something is wrong!</span>
	</body>
	```