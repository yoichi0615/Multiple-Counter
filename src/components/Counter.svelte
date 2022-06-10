<div class="counter-item">
  <input type="text" bind:value={title} on:keyup="{updateTitle}">
  <span>{count}(トータルカウント)</span>
  <div>
    <button on:click="{addCount}">+</button>
    <button on:click="{subtractCount}">-</button>
    <button on:click="{resetCount}">0</button>
    <button on:click="{deleteCounter}">✖️</button>
  </div>
</div>

<script  lang="ts">
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  // export let count;
  export let options;
  export let index;

  let title = 'new';
	let count= 0;

  function updateTitle() {
    dispatch('updateTitle', {index: index, title: title});
  }
  
  function addCount() :void {
    count++; 
    dispatch('addTotalCount', { cnt: count });
  }

  function subtractCount() :void {
    count--;
    $: if (count < 0) {
	    count = 0;
      return;
    }

    dispatch('sutractTotalCount');
  }

  function resetCount() :number {
    return count = 0;
  }

  function deleteCounter() {
    console.log('á')
    dispatch('deleteCounter', { inx: index });
  }
</script>

<style>
  .counter-item {
    display: flex;
    padding-bottom: 15px;
  }
</style>