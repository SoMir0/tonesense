<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  
  let index = 0;

  const dispatch = createEventDispatcher();

  function changeNote(i) {
    dispatch('change', {
      n: i
    });
    index = i;
  }

  export const resetSelect = () => {
    if(index==0) changeNote(0);
    else changeNote(index-1);
  };
  export let note;
</script>

<aside>
  {#each note as not, i}
    {#if note[index] != null}
      <button class={i == index ? "selected" : ""} on:click={() => {changeNote(i)}}>{not.name}</button>
    {/if}
  {/each}
</aside>

<style>
  aside {
    background: #eee;
    height: 100%;
    display: flex; flex-direction: column;
    overflow-y: scroll;
  }

  aside::-webkit-scrollbar {
    display: none;
  }

  aside button {
    outline: none; border: none;
    font-weigh: bold;
    padding: 1rem;
    margin: 0;
    color: #111;
    background: #eee;
  }

  aside button:hover, aside .selected {
    background: #fff;
  }
</style>
