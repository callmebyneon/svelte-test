# Svelte Basic

> You can test the code in [REPL](https://svelte.dev/repl/)

## 1. 선언적 렌더링
- 중괄호를 사용하여 선언적 렌더링

```svelte
<script>
	let name = 'world';
	let age = 85
	...
</script>

<h1>Hello {name}!</h1>
<h2>
	{age}
</h2>

<!-- 단방향 바인딩 -->
<img scr="" alt="{name}" />
<input type="text" value="{name}" />
```
