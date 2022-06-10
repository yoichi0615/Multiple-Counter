<div class="counter-item">
  <input type="text" bind:value={title} on:keyup="{updateTitle}">
  <span class="number">{count}</span>
  <div>
    <button on:click="{addCount}" class="add">+</button>
    <button on:click="{subtractCount}" class="subtract">-</button>
    <button on:click="{resetCount}" class="reset">0</button>
    <button on:click="{deleteCounter}" class="delete">✖️</button>
  </div>
</div>


<script  lang="ts">
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  export let title
  export let index;

  title = 'new';
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

  function resetCount() :void {
    dispatch('resetTotalCount', {cnt: count})
    count = 0;
  }

  function deleteCounter() {
    dispatch('deleteCounter', { inx: index, cnt: count });
  }
</script>

<style>
  .counter-item {
    margin-top: 2rem;
    display: flex;
    padding-bottom: 15px;
    margin: 0 auto;
    justify-content:center;
    background-color: bisque;
    border-bottom: solid 2px orange;
  }

  button {
    margin: 0;
    padding: 0.5rem;
    color: aliceblue;
  }

  .number {
    font-size: 1.5rem;
    margin: 0 2rem;
  }

  .add {
    background-color: palevioletred;
  }

  .subtract {
    background-color: rgba(66,153,225);
  }
  
  .reset {
    background-color: rgba(236,201,75);
  }
</style>