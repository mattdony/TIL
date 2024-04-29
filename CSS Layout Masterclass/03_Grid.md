> Flexbox보다 행과 열을 더 정교하게 배치할 수 있으며, 레이아웃을 구축하는데 있어 CSS의 핵심이다.

### Columns and Rows
- 원하는 크기를 선언하는 것만으로 기본 레이아웃(행과 열)을 설정할 수 있다.
	- `grid-template-columns`: 열의 갯수와 크기를 설정
	- `grid-template-rows`: 행의 갯수와 크기를 설정
- 예시 (2 x 3 크기의 레이아웃 설정)
	```css
	/* style.css */
	.parents {
	display: grid;
	grid-template-columns: 100px 200px 50px;
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
	![[CSS Layout Masterclass/assets/grid_fig01.png]]
	- Grid 경우 사용자가 선언한 행과 열을 구분하기 위한 구분선이 생기게 되면 각각 번호를 갖게 된다.
		- 열(column) 라인: ➡️ (왼쪽 > 오른쪽) 방향으로 1부터 시작해 1씩 증가하는 오름차순의 라인번호를 갖게됨
		- 행(row) 라인: ⬇️ (위 > 아래) 방향으로 1부터 시작해 1씩 증가하는 오름차순의 라인번호를 갖게됨
		- 열(column) 라인 역방향: ⬅️ (오른쪽 > 왼쪽) 방향으로 -1부터 시작해 1씩 감소하는 내림차순의 라인번호를 갖게됨
		- 행(row) 라인 역방향: ⬆️ (아래 > 위) 방향으로 -1부터 시작해 1씩 감소하는 내림차순의 라인번호를 갖게됨

<br>

### Grid Lines
- Grid를 통해 그려지는 요소들은 기본적으로 (1 x 1)의 크기로 순서대로 배치되지만 grid line을 활용해 속성을 활용해 손쉽게 원하는 크기와 위치에 배치시킬 수 있다.
- 다음의 속성을 자식 요소에 선언해 배치를 설정한다.
	- `gird-column-start`: 해당 요소의 열 시작 번호 입력
	- `gird-column-end`: 해당 요소의 열 끝 번호 입력
	- `grid-column`: 해당 요소의 열 시작, 끝 번호 입력
	- `gird-row-start`: 헤당 요소의 행 시작 번호 입력
	- `gird-row-end`: 해당 요소의 행 끝 번호 입력
	- `grid-row`: 해당 요소의 행 시작, 끝 번호 입력
- 라인 번호는 순방향(양수) 또는 역방향(음수) 모두 입력 가능
	```css
	/* style.css */
	.parents {
	display: grid;
	grid-template-columns: 100px 200px 50px;
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

	.child:first-child {
	grid-row-start: 1;
	grid-row-end: -1;
	/* grid-row: 1 / -1; 위의 두 줄과 같은 기능 */
	}

	.child:last-child {
	grid-column-start: 2;
	grid-column-end: 4;
	/* grid-column: 2 / 4; 위의 두 줄과 같은 기능 */
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
	![[CSS Layout Masterclass/assets/grid_fig02.png]]

<br>

### Line Names
- Grid 라인은 기본적으로 라인 번호를 갖지만 특정 이름을 지정해 줄 수 도 있다.
	```css
	/* style.css */
	.parents {
	display: grid;
	grid-template-columns: [apple] 100px [banana] 200px [grape] 50px [melon];
	grid-template-rows: [kor] 200px [jap] 100px [chn];
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

	.child:first-child {
	grid-row: kor / chn;
	}

	.child:last-child {
	grid-column: banana / melon;
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
	![[CSS Layout Masterclass/assets/grid_fig03.png]]