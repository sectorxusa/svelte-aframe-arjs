<script>
	import { onMount } from 'svelte';

	let mounted;
	let aframe;
	let ar;
	$: ready = aframe && ar && mounted;

	const aframeLoaded = () => {
		console.log('aframe');
		aframe = true;
	};

	const arLoaded = () => {
		console.log('ar');
		ar = true;
	};

	onMount(() => {
		console.log('mounted');
		mounted = true;
	});

	let width = 640;
	let height = 480;
</script>

<svelte:head>
	{#if mounted}
		<script
			src="https://aframe.io/releases/1.0.0/aframe.min.js"
			on:load={aframeLoaded}></script>
		<script
			src="https://raw.githack.com/AR-js-org/AR.js/ES6/aframe/build/aframe-ar.js"
			on:load={arLoaded}></script>
	{/if}
</svelte:head>

{#if ready}
	<a-scene
		embedded
		arjs="sourceWidth: window.innerWidth > window.innerHeight ? {width} : {height}; sourceHeight: window.innerWidth > window.innerHeight ? {height} : {width}"
	>
		<a-marker preset="hiro">
			<a-box
				position="0 0.5 0"
				material="opacity: 0.5; side: double;color:blue;"
			>
				<a-torus-knot
					radius="0.26"
					radius-tubular="0.05"
					animation="property: rotation; to:360 0 0; dur: 5000; easing: linear; loop: true"
				/>
			</a-box>
		</a-marker>
		<a-entity camera />
	</a-scene>
{/if}

<style>
	:global(html, body) {
		height: 100%;
		margin: 0;
		overflow: hidden;
	}

	:global(body) {
		position: relative;
	}

	:global(.a-canvas, #arjs-video) {
		display: block;
		width: 100% !important;
		height: 100% !important;
		margin: 0 !important;
		object-fit: contain !important;
	}
</style>
