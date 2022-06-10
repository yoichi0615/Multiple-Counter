<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

	function addNewCounter() {
    dispatch('addNewCounter');
	}
</script>

<button on:click="{addNewCounter}">new counter</button>

<style>
  button {
    margin-top: 1rem;
    color: white;
    background-color: green;
  }
</style>