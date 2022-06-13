<script lang="ts">
	// imports
	import Nav from './components/nav.svelte';
	import Sidebar from './components/sidebar.svelte';

	// definitions
	let userPrefersDark : boolean = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches;
	
	let sidebarController : any;
	
	let index : number = 0;
	let notes = [
	  {name:"note1", content: "Hey this is the first note"},
	  {name:"note2", content: "Hey this is the second note"},
	  {name:"test note", content: "25 all"},
	  {name:"Game", content: "Detroit: Become Human"},
	  {name:"Song", content: "Anything by M.O.O.N really"},
	].reverse();
	
	let menuSize = 0;
	$: cssVarStyles = `--menu-size:${menuSize}`;

	// functions
	if(userPrefersDark && !window.document.body.classList.contains('dark')) window.document.body.classList.toggle('dark');
	function toggle() {
    userPrefersDark = !userPrefersDark;
    window.document.body.classList.toggle('dark');
  }

	const getFormattedTime = () => {
	  let now = new Date();
	  return now.getDate() + "." + (now.getMonth()+1) + "." + now.getFullYear() + "\n" + "note" + (notes.length+1).toString();
	}
  
	function handleNote(e : Event) {
	  index = e.detail.n;
	}
  
	function handleAdd() {
	  notes.push({name:getFormattedTime(), content:"test text"});
	  notes = notes;
	}
  
	function handleDelete() {
	  notes.splice(index, 1);
	  notes = notes;
	  sidebarController();
	}

	function handleMenu() {
		menuSize = (menuSize == 0) ? 1 : 0;
	}
  </script>
  
  <main style="{cssVarStyles}">
	<div class="nav">
	  <Nav darkTheme={userPrefersDark} on:delete={handleDelete} on:add={handleAdd} on:toggle={toggle} on:menu={handleMenu} />
	</div>
	<div class="side">
	  <Sidebar note={notes} on:change={handleNote} bind:resetSelect={sidebarController} />
	</div>
	{#if notes[index] != null}
	<textarea class="text" bind:value={notes[index].content}></textarea>
	{:else}
	<p>No notes to show!</p>
	{/if}
	<div class="config">
		<input type="checkbox"/>
		<label for="checkbox">Autosave</label>
		<button>clickyyy</button>
	</div>
  </main>
  
  <style>
	:global(html), :global(body) {
	  height: 100%; width: 100%;
	  margin: 0; padding: 0;
	  font-family: sans-serif;
	}

	:root {
		--white: #fff;
		--gray: #808080;
		--gray-light: #eee;
		--gray-dark: #dfdfdf;
		--black: #111;
	}
  
	main {
	  height: 100vh;
	  display: grid;
	  grid-template-areas:
	  "nav nav nav"
	  "side text text"
	  "side text text";
	  grid-template-rows: 0.2fr 1fr 1fr;
	  grid-template-columns: 10rem 1fr 1fr;
	  background: var(--white);
	}
  
	main p {
	  position: relative; left: 50%; top: 50%;
	  user-select: none;
	  color: var(--gray);
	  text-align:center;
	}
  
	.nav {
	  grid-area: nav;
	}
  
	.side {
	  grid-area: side;
	}
  
	.text {
	  grid-area: text;
	}

	.config {
		display: flex; flex-direction: column; align-items: center;
		position: absolute;
		top: 4rem;
		right: 2rem;
		padding: 1rem;
		gap: 1rem;
		border-radius: 0.125rem;
		background: var(--gray-light);
		transform: scale(var(--menu-size));
		transition: transform 0.3s;
	}
  
	textarea {
	  resize: none;
	  outline: none; border: none;
	  background: var(--white);
		color: var(--black);
	}
  
	@media only screen and (max-width: 600px) {
	  main {
			grid-template-areas: 
		  	"nav"
		  	"side"
		  	"text";
			grid-template-rows: 0.1fr 0.1fr 1fr;
			grid-template-columns: 1fr;
	  }
	  
	  .side {
			max-height: 15vh;
	  }
	}

	:global(body.dark) {
		--white: #111;
		--gray: #808080;
		--gray-light: #323232;
		--gray-dark: #222;
		--black: #eee;
	}
  </style>
  
