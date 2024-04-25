> Flexbox보다 행과 열을 더 정교하게 배치할 수 있으며, 레이아웃을 구축하는데 있어 CSS의 핵심이다.

### Columns and Rows
- 기본 레이아웃(행과 열)을 설정
	- `grid-template-columns`: 열의 갯수와 크기를 설정
	- `grid-template-rows`: 행의 갯수와 크기를 설정
- 예시 (2 x 2 크기의 레이아웃 설정)
	```css
	/* style.css */
	.parents {
	display: grid;
	grid-template-columns: 100px 200px;
	grid-template-rows: 200px 100px;
	gap: 10px;
	}

	.child {
	background-color: tomato;
	display: flex;
	justify-content: center;
	align-items: center;
	color: white;
	font-size: 30px;
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
