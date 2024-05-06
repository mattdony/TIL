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

### @extend
