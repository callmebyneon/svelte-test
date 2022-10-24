# Svelte Basic

> You can test the code in [REPL](https://svelte.dev/repl/)

## 1. 선언적 렌더링
### a. 선언적 렌더링과 데이터 바인딩
- 중괄호를 사용하여 선언적 렌더링
- 바인딩 되는 속성 앞에 `bind:`를 추가하여 `script`의 변수와 html 태그의 속성을 양방향으로 바인딩

```svelte
<script>
	let name = 'world';
	let age = 85
	function assign() {
		name = 'Heropy'
		age = 36
	}
</script>

<h1>Hello {name}!</h1>
<h2>
	{age}
</h2>

<!-- 단방향 바인딩 -->
<img scr="" alt="{name}" />
<!-- <img scr="" alt={name} /> -->

<!-- 양방향 바인딩 -->
<input type="text" bind:value="{name}" />
<!-- <input type="text" bind:value={name} /> -->

<button on:click={assign}>
	Assign
</button>
```

### b. 조건부 렌더링
- 조건부로 스타일을 적용시 `{}`안에 삼항연산자를 사용하여 적용 가능
```svelte
...

<h2 class={age < 85 ? 'active' : ''}>
	{age}
</h2>

...

<style>
	h1 {
		color: red;
	}
	.active {
		color: blue;
	}
</style>
```

## 2. 조건문과 반복문
### a. 조건문
```svelte
<script>
	let name = 'world';
	let toggle = false;
</script>

<button on:click={() => {toggle = !toggle}}>
	Toggle
</button>
{#if toggle}
	<h1>Hello {name}!</h1>
{:else}
	<div>No name!</div>
{/if}
```

### b. 반복문
```svelte
<script>
	let fruits = ['Apple', 'Banana', 'Cherry', 'Orange', 'Mango']
</script>

<ul>
	{#each fruits as fruit}
	  <li>{fruit}</li>
	{/each}
</ul>
```

## c. 반복문에서의 반응성 확인
```svelte
<script>
  ...

  function deleteFruit() {
		fruits = fruits.slice(1)
	}
</script>

...

<button on:click={deleteFruit}>
	Eat it!
</button>
```


## 3. 이벤트 핸들링
### a. Basic
- `on:` 키워드(directive) + 이벤트 종류 (예. click, mouseenter ...)
```svelte
<script>
	...
	
	function enter() {
		name = 'enter'
	}
	
	function leave(newName) {
		name = newName
	}
</script>

...

<div 
  class="box"
  style="background-color: {isRed ? 'red' : 'orange'}"
  on:click={() => { isRed = !isRed }}
  on:mouseenter={enter}
  on:mouseleave={() => leave('leave')}
  >Box!</div>

...
```

### b. 양방향 입력 바인딩
- 아래 코드 에서 `test-1`처럼 입력된 값과 이벤트를 바인딩 한 예시를 `test-2`와 같이 사용 가능
```svelte
<script>
	let text = ''
</script>

<h1>
	{text}
</h1>

<!-- test-1 -->
<input id="test-1"
       type="text"
			 value={text}
			 on:input={(e) => { text = e.target.value }} />

<!-- test-2 -->
<input id="test-2"
       type="text"
			 bind:value={text} />

<button on:click={() => { text = 'Heropy' }}>
	Click
</button>
```