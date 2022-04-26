<script>
	import { enhance } from '$lib/form';
	import Todo from './Todo.svelte';

	export let todos;
</script>

<svelte:head>
	<title>Todos</title>
	<meta name="description" content="A todo list app" />
</svelte:head>

<div class="todos">
	<h1>Todos</h1>

	<form
		class="new"
		action="/todos"
		method="post"
		use:enhance={{
			result: async ({ form }) => {
				form.reset();
			}
		}}
	>
		<input name="text" aria-label="Add todo" placeholder="+ tap to add a todo" />
	</form>

	{#each todos as todo (todo.uid)}
		<Todo {todo}/>
	{/each}
</div>

<style>
	.todos {
		width: 100%;
		max-width: var(--column-width);
		margin: var(--column-margin-top) auto 0 auto;
		line-height: 1;
	}

	.new {
		margin: 0 0 0.5rem 0;
	}

	input {
		border: 1px solid transparent;
	}

	input:focus-visible {
		box-shadow: inset 1px 1px 6px rgba(0, 0, 0, 0.1);
		border: 1px solid #ff3e00 !important;
		outline: none;
	}

	.new input {
		font-size: 28px;
		width: 100%;
		padding: 0.5em 1em 0.3em 1em;
		box-sizing: border-box;
		background: rgba(255, 255, 255, 0.05);
		border-radius: 8px;
		text-align: center;
	}
</style>
