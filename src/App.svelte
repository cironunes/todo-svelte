<script>
	let newTodo = '';
	export let todos = [
		{
			text: 'Go to mall',
			done: true,
		},
		{
			text: 'Study Svelte',
			done: false
		},
	];
</script>

<style>
.done {
	text-decoration: line-through;
}
</style>

<form on:submit={(e) => {
	e.preventDefault();
	if (newTodo === '') return;
	todos = [...todos, { text: newTodo, done: false }];
	newTodo = '';
}}>
	<div>
		<label>
			<span>What do I have to do</span>
			<input type="text" bind:value={newTodo}>
		</label>
	</div>
	<button>Create</button>
</form>

<ul>
	{#each todos as { done, text }}
		<li class="{done && 'done'}">
			<label>
				<input type="checkbox" bind:checked={done} />
				<span>{text}</span>
			</label>
		</li>
	{/each}
</ul>

<p>Remaining: {todos.filter(item => !item.done).length}</p>
