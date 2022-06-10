<div>
	<h1>Multiple Counter</h1>
	{#if options}
		{#each options as option, i}
		<span>{i}</span>	
			<!-- <svelte:component this={option.component} on:updateTotalCount={updateTotalCount} index={option.index} on:deleteCounter={deleteCounter}/> -->
			<Counter on:addTotalCount={addTotalCount} index={i} options={options} on:deleteCounter={deleteCounter} on:sutractTotalCount={sutractTotalCount} on:updateTitle={updateTitle}/>
		{/each}
	{/if}
	<AddNewCounter options={options} on:addNewCounter={addNewCounter}/>
	
	<p>
		title lists:
		{#each options as option, i}
		{option.title + ','}
		{/each}
	</p>
	<p>total count: {totalCount}</p>
</div>


<script lang="ts">
	import Counter from './components/Counter.svelte';
	import AddNewCounter from './components/AddNewCounter.svelte';
	let options = [
		{
			index: 0,
			title: 'new'
		},
	];

	let titles = [];

	let totalCount = 0
	$: if (totalCount < 0) {
	totalCount = 0;
  }

	function updateTitle(value) {
		console.log(value)
		let index = value.detail.index;
		options[index].title = value.detail.title;
		options = options
	}
	
	function addTotalCount(val :any) {
		totalCount += 1;
	}

	function sutractTotalCount(val :any){
		totalCount -= 1;
	}

	function addNewCounter(val) {
		options.push({
			index: options.length,
			title: 'new'
		});
    options = options;
		console.log('af');
	}

	function deleteCounter(val :any) 
	{
		options.splice(val.detail.inx, 1);
		options = options;
	}
</script>