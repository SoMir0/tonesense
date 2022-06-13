<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  
  import PlusCircle from "svelte-bootstrap-icons/lib/PlusCircle";
  import Trash from "svelte-bootstrap-icons/lib/Trash";
  import Wrench from "svelte-bootstrap-icons/lib/Wrench";
  import Sun from "svelte-bootstrap-icons/lib/Sun";
  import Moon from "svelte-bootstrap-icons/lib/Moon";

  const dispatch = createEventDispatcher();
  
  function addNote() {
    dispatch('add');
  }

  function deleteNote() {
    dispatch('delete');
  }

  function changeTheme() {
    dispatch('toggle');
  }

  function enableMenu() {
    dispatch('menu');
  }

  export let darkTheme;
</script>

<nav>
  <button on:click={addNote}><PlusCircle width={18} height={18} /></button>
  <button on:click={deleteNote}><Trash width={18} height={18} /></button>
  <button on:click={changeTheme}>
    {#if darkTheme}
      <Sun width={18} height={18} />
    {:else}
      <Moon width={18} height={18} />
    {/if}
  </button>
  <button on:click={enableMenu}><Wrench width={18} height={18} /></button>
</nav>

<style>
  nav {
    display: flex; justify-content: space-evenly; align-items: center;
    background: var(--gray-dark); height: 100%;
  }

  nav button {
    outline: none; border: none; background: #0000;
    cursor: pointer;
    width: 100%; height: 100%;
    padding: 1rem;
    color: var(--black);
  }
</style>
