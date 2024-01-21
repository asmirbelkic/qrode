<script>
	import { onMount } from "svelte";
	import QRCode from "qrcode";
	import Code from "./Code.svelte";
	let text = "";
	let canvas;
	let base64;

	onMount(() => {
		updateQRCode();
	});

	async function updateQRCode() {
		if (!canvas) return;

		if (text) {
			await generateQRCode();
		} else {
			clearCanvas();
			base64 = null;
		}
	}

	async function generateQRCode() {
		try {
			const qrOptions = {
				width: 1200,
				height: 1200,
				margin: 0,
				color: {
					dark: "#000", // Couleur des pixels (blanc)
					light: "#fff", // Couleur de fond (noir)
				},
			};
			await QRCode.toCanvas(canvas, text, qrOptions);
			base64 = await QRCode.toDataURL(text, qrOptions);
		} catch (error) {
			console.error(error);
		}
	}

	function clearCanvas() {
		const context = canvas.getContext("2d");
		context.clearRect(0, 0, canvas.width, canvas.height);
	}
</script>

<main>
	<div>
		<h5>Enter a url to create a QR code</h5>
		<input type="text" placeholder="https://your-website.com" maxlength="256" bind:value={text} on:input={updateQRCode} />
	</div>
	<Code bind:canvas {base64} />
</main>

<style>
	:global(body) {
		margin: 0;
		background-color: #fff;
		font-family: Inter, sans-serif;
		font-feature-settings:
			"liga" 1,
			"calt" 1;
		color: #fff;
		font-size: 14px;
		line-height: 20px;
	}
	:global(*) {
		box-sizing: border-box;
		font-family: inherit;
	}
	:global(h5) {
		margin-bottom: 1rem;
		margin-top: 0;
		font-weight: 600;
		margin-bottom: 1.2em;
		font-size: 1.25rem;
		color: #000;
		line-height: 1;
	}
	main {
		display: grid;
		width: 100%;
		max-width: 80em;
		min-height: 100vh;
		margin-right: auto;
		margin-left: auto;
		padding: 3.4em;
		justify-content: center;
		align-items: center;
		grid-auto-columns: 1fr;
		grid-column-gap: 4em;
		grid-row-gap: 2em;
		grid-template-columns: 1.5fr 1fr;
		grid-template-rows: auto;
	}
	@media screen and (max-width: 991px) {
		main {
			max-width: 38em;
			padding-right: 5%;
			padding-left: 5%;
			justify-content: center;
			align-content: center;
			grid-template-columns: 1fr;
		}
	}
	input {
		height: 3rem;
		margin-bottom: 0px;
		display: block;
		width: 100%;
		font-weight: 500;
		padding: 0px 1.2rem;
		border: 1px solid transparent;
		border-radius: 0.5rem;
		background-color: #f5f4f4;
		color: #000;
		font-size: 1.25rem;
		line-height: 1;
		outline: none;
	}
	input:focus {
		background-color: #f1f0f0;
	}
</style>
