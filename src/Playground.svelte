<script>
	import { quintOut } from 'svelte/easing';
	import { crossfade, fly, slide } from 'svelte/transition';

  import Tray from './Tray.svelte';
  import TrayHolder from './TrayHolder.svelte';
  import TrayButton from './TrayButton.svelte';

	const [send, receive] = crossfade({
		duration: d => Math.sqrt(d * 200),

		fallback(node, params) {
			const style = getComputedStyle(node);
			const transform = style.transform === 'none' ? '' : style.transform;

			return {
				duration: 600,
				easing: quintOut,
				css: t => `
					transform: ${transform} scale(${t});
					opacity: ${t}
				`
			};
		}
	});

	let uid = 1;

	let todos = [
		{ id: uid++, done: false, description: 'write some docs' },
		{ id: uid++, done: false, description: 'start writing blog post' },
		{ id: uid++, done: true,  description: 'buy some milk' },
		{ id: uid++, done: false, description: 'mow the lawn' },
		{ id: uid++, done: false, description: 'feed the turtle' },
		{ id: uid++, done: false, description: 'fix some bugs' },
	];

	function add(input) {
		const todo = {
			id: uid++,
			done: false,
			description: input.value
		};

		todos = [todo, ...todos];
		input.value = '';
	}

	function remove(todo) {
		todos = todos.filter(t => t !== todo);
	}

	function mark(todo, done) {
		todo.done = done;
		remove(todo);
		todos = todos.concat(todo);
  }
  
  let visible = true;
  let tray1out = false;
</script>

<style>
	.board {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-gap: 1em;
		max-width: 36em;
		margin: 0 auto;
	}

	.board > input {
		font-size: 1.4em;
		grid-column: 1/3;
	}

	h2 {
		font-size: 2em;
		font-weight: 200;
		user-select: none;
		margin: 0 0 0.5em 0;
	}

	label {
		position: relative;
		line-height: 1.2;
		padding: 0.5em 2.5em 0.5em 2em;
		margin: 0 0 0.5em 0;
		border-radius: 2px;
		user-select: none;
		border: 1px solid hsl(240, 8%, 70%);
		background-color:hsl(240, 8%, 93%);
		color: #333;
	}

	input[type="checkbox"] {
		position: absolute;
		left: 0.5em;
		top: 0.6em;
		margin: 0;
	}

	.done {
		border: 1px solid hsl(240, 8%, 90%);
		background-color:hsl(240, 8%, 98%);
	}

	button {
		position: absolute;
		top: 0;
		right: 0.2em;
		width: 2em;
		height: 100%;
		background: no-repeat 50% 50% url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24'%3E%3Cpath fill='%23676778' d='M12,2C17.53,2 22,6.47 22,12C22,17.53 17.53,22 12,22C6.47,22 2,17.53 2,12C2,6.47 6.47,2 12,2M17,7H14.5L13.5,6H10.5L9.5,7H7V9H17V7M9,18H15A1,1 0 0,0 16,17V10H8V17A1,1 0 0,0 9,18Z'%3E%3C/path%3E%3C/svg%3E");
		background-size: 1.4em 1.4em;
		border: none;
		opacity: 0;
		transition: opacity 0.2s;
		text-indent: -9999px;
		cursor: pointer;
	}

	label:hover button {
		opacity: 1;
	}
  
  .container {
    position: relative;
    width: 50%;
    height: 320px;
    border: 1px solid black;
  }

  .contained {
    position: absolute;
    /* left: 0; */
  }

  .box {
    width: 100%;
    height: 145px; 
    border: 1px solid black;
  }

  .bottom-right {
    position: absolute;
    bottom: 0px;
    right: 2px;
  }

  .tray-0 {
    position: absolute;
    top: 0px;
  }
  .tray-1 {
    position: absolute;
    top: 23px;
  }
</style>

<div style='width: inherit; height=inherit;'>
  <TrayHolder>
    <Tray>
      <p>here's</p>
      <p>here's</p>
      <p>here's</p>
      <p>here's</p>
      <p>here's</p>
    </Tray>
    <Tray>
      more down here <br/>
      more down here <br/>
      more down here <br/>
      more down here <br/>
    </Tray>
  </TrayHolder>
</div>

<div style='width: inherit; height=inherit;'>
  <!-- <TrayButton width={20} height={20} fill='#98d02e' stroke='#65b81d' strokeWidth={5} pointDown={true} /> -->
  <TrayButton width={20} height={20} fill='#b81d1d' stroke='#b81d1d' strokeWidth={5} pointDown={true} />
</div>
<div class='container'>
  <div class='contained box tray-1' style='transition: transform 0.8s;{tray1out ? 'transform: translate(0px, 125px);' : ''} background-color:red; '>
    <div class='contained bottom-right'>
      <input type="checkbox" bind:checked={tray1out} style='position:static;'>
    </div>
    <div class='contained' style='position: absolute; bottom: 0px;'>Tray 1</div>
  </div>
  <div class='contained box tray-0' style='background-color:green; '>
    <!-- <div class='contained bottom-right'>
      <input type="checkbox" bind:checked={trayXout} style='position:static;'>
    </div> -->
    <div class='contained' style='position: absolute; bottom: 0px;'>Tray 0</div>
  </div>
  <div class='contained' style='position: absolute; bottom: 0px;'>Tray Container</div>
</div>

<div class='container'>
  {#if visible}
    <div transition:slide="{{delay: 250, duration: 300, easing: quintOut }}">
      slides in and out
    </div>
  {/if}
</div>

<div class='container'>
  <div class='contained' style='background-color:green; '>A</div>
  <div class='contained' style='background-color:red; '>B</div>
  <div class='contained' style='background-color:blue; '>C</div>
  {#each todos as todo}
  <!-- position: relative; left: 10px, top: {todo.id * 100}px; -->
  <div class='contained' id={todo.id} style='top: {todo.id * 100}px;'>
  <p>{todo.description}</p>
  </div>
  {/each}
</div>
  
	
<div class='board'>
  <h1>Playground</h1>
  
  <p>This was based on the <a href='https://svelte.dev/tutorial/deferred-transitions'>Deferred Transitions</a>
  example from the Svelte API docs, but who knows what it is now!</p>
	
  <input
		placeholder="what needs to be done?"
		on:keydown={e => e.key === 'Enter' && add(e.target)}
	>

  <div class='left'>
		<h2>todo</h2>
		{#each todos.filter(t => !t.done) as todo (todo.id)}
			<label in:receive="{{key: todo.id}}" out:send="{{key: todo.id}}">
				<input type=checkbox on:change={() => mark(todo, true)}>
				{todo.description}
				<button on:click="{() => remove(todo)}">remove</button>
			</label>
		{/each}
	</div>

	<div class='right'>
		<h2>done</h2>
		{#each todos.filter(t => t.done) as todo (todo.id)}
			<label class="done" in:receive="{{key: todo.id}}" out:send="{{key: todo.id}}">
				<input type=checkbox checked on:change={() => mark(todo, false)}>
				{todo.description}
				<button on:click="{() => remove(todo)}">remove</button>
			</label>
		{/each}
	</div>
</div>

