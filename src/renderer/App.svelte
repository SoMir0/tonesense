<script lang="ts">
	import Nav from './components/nav.svelte';
	import Sidebar from './components/sidebar.svelte';
	let sidebarController;
	
	let index = 0;
	let notes = [
	  {name:"note1", content: "Hey this is the first note"},
	  {name:"note2", content: "Hey this is the second note"},
	  {name:"test note", content: "25 all"},
	  {name:"Game", content: "Detroit: Become Human"},
	  {name:"Song", content: "Anything by M.O.O.N really"},
	].reverse();
  
	const getFormattedTime = () => {
	  let now = new Date();
	  return now.getDate() + "." + (now.getMonth()+1) + "." + now.getFullYear() + " " + now.getHours() + ":" + now.getMinutes() + ":" + now.getSeconds();
	}
  
	function handleNote(e) {
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
  </script>
  
  <main>
	<div class="nav">
	  <Nav on:delete={handleDelete} on:add={handleAdd} />
	</div>
	<div class="side">
	  <Sidebar note={notes} on:change={handleNote} bind:resetSelect={sidebarController} />
	</div>
	{#if notes[index] != null}
	<textarea class="text" bind:value={notes[index].content}></textarea>
	{:else}
	<p>No notes to show!</p>
	{/if}
  </main>
  
  <style>
	:global(html), :global(body) {
	  height: 100%; width: 100%;
	  margin: 0; padding: 0;
	  font-family: sans-serif;
	}
  
	main {
	  height: 100vh;
	  display: grid;
	  grid-template-areas:
	  "nav nav nav"
	  "side text text"
	  "side text text";
	  grid-template-rows: 0.2fr 1fr 1fr;
	  grid-template-columns: 0.45fr 1fr 1fr;
	}
  
	main p {
	  position: relative; left: 50%; top: 50%;
	  user-select: none;
	  color: gray;
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
  
	textarea {
	  resize: none;
	  outline: none; border: none;
	  background: #fff;
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
  </style>
  