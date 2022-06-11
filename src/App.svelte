<script lang="ts">
	import Counter from './components/Counter.svelte';
	import AddNewCounter from './components/AddNewCounter.svelte';

  type updateEventType = {
    index: number,
  	title: string,
    cnt: number
  }

  type eventType = {
    index: number,
    cnt: number
  }

	type contentsType = {
  	title: string,
  	count: number,
	};

	let contents: contentsType[]= [
		{
			title: 'new',
			count: 0
		}
	];

	let totalCount: number = 0
	if (totalCount < 0) {
		totalCount = 0;
  }

	function updateTitle(value: CustomEvent<updateEventType>): void {
		contents[value.detail.index].title = value.detail.title;
	}
	
	function addTotalCount(value: CustomEvent<eventType>): void {
		contents[value.detail.index].count = value.detail.cnt;
		totalCount++;
	}

	function subtractTotalCount(value: CustomEvent<eventType>): void {
		contents[value.detail.index].count = value.detail.cnt;
		totalCount--;
	}

	function addNewCounter(): void {
		contents.push({
			title: 'new',
			count: 0
		});
    contents = contents;
	}

	function deleteCounter(value: CustomEvent<eventType>): void {
		contents.splice(value.detail.index, 1);
		contents = contents;
		totalCount -= value.detail.cnt
	}

	function resetTotalCount(value: CustomEvent<eventType>): void {
		contents[value.detail.index].count = 0;
		totalCount -= value.detail.cnt;
	}
</script>

<div class=text-center>
	<h1>Multiple Counter</h1>
	{#if contents}
		{#each contents as content, i}	
			<Counter on:addTotalCount={addTotalCount} index={i} content={content} count={content.count} on:deleteCounter={deleteCounter} on:subtractTotalCount={subtractTotalCount} on:updateTitle={updateTitle} on:resetTotalCount={resetTotalCount}/>
		{/each}
	{/if}
	<AddNewCounter on:addNewCounter={addNewCounter}/>
	<p>
		title lists:
		{#each contents as content, i}
			{content.title}
		{#if (i + 1 in contents) && contents[i + 1].title !== '' && content.title !== ''}
			,
		{/if}
		{/each}
	</p>
	<p>total count: {totalCount}</p>
</div>

<style>
	.text-center {
		text-align: center;
	}
</style>