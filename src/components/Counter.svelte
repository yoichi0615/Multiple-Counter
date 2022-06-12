<script  lang="ts">
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher<{updateTitle: updateEventType, 
    addTotalCount: eventType, 
    subtractTotalCount: eventType, 
    resetTotalCount: eventType, 
    deleteCounter: eventType
  }>();

  type contentsType = {
  	title: string,
  	count: number,
	};

  type updateEventType = {
    index: number,
  	title: string,
    cnt: number
  }

  type eventType = {
    index: number,
    cnt: number
  }

  export let index: number;
  export let content: contentsType
  export let count: number;
  
  function updateTitle(): void {
    dispatch('updateTitle', {
      index: index, 
      title: content.title,
      cnt: count
    });
  }
  
  function addCount(): void {
    count++
    dispatch('addTotalCount', {
      index: index, 
      cnt: count
    });
  }

  function subtractCount(): void {
    count--
    if (count < 0) {
	    count = 0;
      return;
    }

    dispatch('subtractTotalCount', {
      index: index, 
      cnt: count
    })
  }

  function resetCount(): void {
    dispatch('resetTotalCount', {
      index: index, 
      cnt: count
    })
    count = 0;
  }

  function deleteCounter(): void {  
    dispatch('deleteCounter', {
      index: index,
      cnt: count
    })
  }
</script>

<div class="counter-item">
  <input type="text" bind:value={content.title} on:keyup="{updateTitle}">
  <span class="number">{content.count}</span>
  <div>
    <button on:click="{addCount}" class="add">+</button>
    <button on:click="{subtractCount}" class="subtract">-</button>
    <button on:click="{resetCount}" class="reset">0</button>
    <button on:click="{deleteCounter}" class="delete">✖️</button>
  </div>
</div>

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