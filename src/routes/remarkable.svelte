<script>
	let md;
	let value = 'Hello, **world**!';

	const initializeRemarkable = () => {
		md = new window.remarkable.Remarkable();
	};
</script>

<svelte:head>
	<script
		src="https://cdnjs.cloudflare.com/ajax/libs/remarkable/2.0.0/remarkable.min.js"
		on:load={initializeRemarkable}></script>
</svelte:head>

<div className="MarkdownEditor">
	<h3>Input</h3>
	<label htmlFor="markdown-content"> Enter some markdown </label>
	<textarea id="markdown-content" bind:value />
	<h3>Output</h3>
	<div className="content">
		{#if md}
			{@html md.render(value)}
		{/if}
	</div>
</div>
