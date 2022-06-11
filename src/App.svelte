<div class=text-center>
	<h1>Multiple Counter</h1>
	{#if contents}
		{#each contents as content, i}	
		<Counter on:addTotalCount={addTotalCount} id={content.id} contents={contents} content={content} title={content.title} on:deleteCounter={deleteCounter} on:sutractTotalCount={sutractTotalCount} on:updateTitle={updateTitle} on:resetTotalCount={resetTotalCount}/>
		{/each}
	{/if}
	<AddNewCounter on:addNewCounter={addNewCounter}/>
	
	<p>
		{#if contents.length < 2}
		title list:
		{:else}
		title lists:
		{/if}
		{#each contents as content, i}
		{#if i > 0}
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
			id: 1,
			title: 'new',
			count: 0
		},
	];

	let totalCount = 0
	$: if (totalCount < 0) {
		totalCount = 0;
  }

	function updateTitle(value) 
	{
		let index = value.detail.index;
		contents[index].title = value.detail.title;
		contents = contents
	}
	
	function addTotalCount(val) 
	{
		let index = val.detail.index;
		contents[index].count = val.detail.cnt;
		totalCount += 1;
	}

	function sutractTotalCount() 
	{
		totalCount -= 1;
	}

	function addNewCounter() 
	{
		contents.push({
			id: contents.length + 1,
			title: 'new',
			count: 0
		});
    contents = contents;
	}

	function deleteCounter(val) 
	{
		console.log(contents);
		
		// console.log(val.detail.inx);
		let index = contents.findIndex( (element) => element.id === val.detail.id);
		console.log(index)
		contents.splice(index, 1);
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