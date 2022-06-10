<div class=text-center>
	<h1>Multiple Counter</h1>
	{#if contents}
		{#each contents as content, i}	
		<Counter on:addTotalCount={addTotalCount} index={i} title={content.title} on:deleteCounter={deleteCounter} on:sutractTotalCount={sutractTotalCount} on:updateTitle={updateTitle} on:resetTotalCount={resetTotalCount}/>
		{/each}
	{/if}
	<AddNewCounter on:addNewCounter={addNewCounter}/>
	
	<p>
		title lists:
		{#each contents as content, i}
		{#if content.index > 0}
		,
		{/if}
		{content.title}
		{/each}
	</p>
	<p>total count: {totalCount}</p>
</div>

<script lang="ts">
	import Counter from './components/Counter.svelte';
	import AddNewCounter from './components/AddNewCounter.svelte';
	let contents = [
		{
			index: 0,
			title: 'new'
		},
	];

	let totalCount = 0
	$: if (totalCount < 0) {
		totalCount = 0;
  }

	function updateTitle(value) 
	{
		console.log(value)
		let index = value.detail.index;
		contents[index].title = value.detail.title;
		contents = contents
	}
	
	function addTotalCount() 
	{
		totalCount += 1;
	}

	function sutractTotalCount() 
	{
		totalCount -= 1;
	}

	function addNewCounter() 
	{
		contents.push({
			index: contents.length,
			title: 'new'
		});
    contents = contents;
	}

	function deleteCounter(val) 
	{
		console.log(val.detail.inx);
		contents.splice(val.detail.inx, 1);
		console.log(contents)
		contents = contents;
		totalCount -= val.detail.cnt
	}

	function resetTotalCount(val) 
	{
		totalCount -= val.detail.cnt;
	}
</script>

<style>
	.text-center {
		text-align: center;
	}
</style>