<script>
	export let canvas;
	export let base64;
</script>

<main>
	<canvas width="1200" height="1200" bind:this={canvas} style={base64 ? 'display:none' : null}></canvas>
	<img src={base64} alt="" style={base64 ? 'display:block' : 'display:none'} />
</main>

<style>
	main {
		padding-top: 100%;
		background-color: #f5f4f4;
		width: 100%;
		margin-right: auto;
		position: relative;
		margin-left: auto;
	}
	canvas {
		position: absolute;
    top: 0px;
    left: 0px;
    width: 100%;
    height: 100%;
	}
	img {
		max-width: 100%;
		vertical-align: middle;
		display: inline-block;
		position: absolute;
    top: 0px;
    left: 0px;
    width: 100%;
    height: 100%;
	}
</style>
