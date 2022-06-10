<button on:click="{addNewCounter}">new Counter</button>


<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  export let options;
	import Counter from './Counter.svelte';
	function addNewCounter() {
    dispatch('addNewCounter');
	}
</script>
