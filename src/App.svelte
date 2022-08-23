<script lang="ts">
	import domtoimage from "dom-to-image-more";

	import Input from "./lib/Input.svelte";

	let text = "Hello World!";
	let text_color = "#222222";
	let background_color = "#ffcccc";
	let background_image =
		"/* images must be base64 encoded */ linear-gradient(43deg, #4158D0 0%, #C850C0 46%, #FFCC70 100%)";
	let font_size = "48";
	let font_weight = "600";
	let padding = "32";
	let justify_content = "center";
	let align_items = "center";

	async function createImage() {
		const element = document.getElementById("wrapper");
		const base64Img = await domtoimage.toPng(element, {
			width: 1200,
			height: 630,
		});

		return base64Img;
	}

	async function openImageInTab() {
		const url = await createImage();
		window.open(url, "_blank")
	}

	async function copyImageLink() {
		let url = await createImage();
		navigator.clipboard.writeText(url);
	}
</script>

<h1 style="color:#f00;text-align:center;font-size:2rem;">
	You need to download the images for use.
	<br />
	Not mobile responsive.
</h1>

<div class="page">
	<div class="settings">
		<Input name="text" label="Text:" bind:value={text} />
		<Input
			name="text-color"
			label="Text color:"
			type="color"
			bind:value={text_color}
		/>
		<Input
			name="background-color"
			label="Background color:"
			type="color"
			bind:value={background_color}
		/>
		<Input
			name="background-image"
			label="Background image:"
			bind:value={background_image}
		/>

		<Input
			name="font-size"
			label="Font size (px):"
			type="number"
			bind:value={font_size}
		/>
		<Input
			name="font-weight"
			label="Font weight:"
			type="number"
			bind:value={font_weight}
		/>
		<Input
			name="padding"
			label="Padding (px):"
			type="number"
			bind:value={padding}
		/>

		<div>
			<label for="align-items">Vertical align (text):</label>
			<select name="align-items" bind:value={align_items}>
				<option value="flex-start">Top</option>
				<option value="center">Center</option>
				<option value="flex-end">Bottom</option>
			</select>
		</div>

		<div>
			<label for="justify-content">Horizontal align (text):</label>
			<select name="justify-content" bind:value={justify_content}>
				<option value="flex-start">Left</option>
				<option value="center">Center</option>
				<option value="flex-end">Right</option>
			</select>
		</div>
	</div>

	<div>
		<div
			id="wrapper"
			style="
		--background-color:{background_color}; 
		--background-image: {background_image};
		--padding:{`${padding}px`};
		--align-items:{align_items}; 
  	--justify-content:{justify_content}; 
		--text-color:{text_color};
  	--font-size:{`${font_size}px`};
		--font-weight:{font_weight};
  "
		>
			{text}
		</div>
		<div>
			<button on:click={openImageInTab}>Open image in new tab</button>
			<button on:click={copyImageLink}>Copy image link</button>
		</div>
	</div>
</div>

<style>
	#wrapper {
		background-color: var(--background-color);
		background-image: var(--background-image);
		background-repeat: no-repeat;
		background-position: center;

		color: var(--text-color);
		font-size: var(--font-size);
		font-weight: var(--font-weight);

		width: 1200px;
		height: 630px;

		display: flex;
		align-items: var(--align-items); /* Vertical align */
		justify-content: var(--justify-content); /* Horizontal align */

		padding: var(--padding);
	}

	.settings {
		display: flex;
		flex-direction: column;
		width: 40%;
		gap: 20px;
		margin: 2rem 0;
	}

	.page {
		/* display: flex;
		flex-direction: column;
		gap: 6rem; */
		width: fit-content;
		margin: 0 auto;
	}
</style>
