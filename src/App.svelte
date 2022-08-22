<script>
	import html2canvas from "html2canvas";

	import Input from "./lib/Input.svelte";

	let text = "Hello World!";
	let text_color = "#222222";
	let font_size = "48";
	let font_weight = "bold";
	let background = "#ffcccc url(https://bit.ly/3SKVrcF) no-repeat center";
	let padding = "32";
	let justify_content = "center";
	let align_items = "center";

	async function createImage() {
		const element = document.getElementById("wrapper");
		const img = await html2canvas(element, {
			scale: 2,
			allowTaint: true,
		});

		// @ts-ignore
		const img_blob = new Blob([img], { type: "image/png" });
		const img_url = URL.createObjectURL(img_blob);

		document.body.appendChild(img);

		console.log(img_url);
		return img_url;
	}

	async function openImageInTab() {
		createImage();
		console.log("open");
	}
	function copyImageLink() {
		createImage();
		console.log("copy");
	}
</script>

<h1 style="color:#f00;text-align:center;font-size:2rem;">
	No way to generate image yet and not mobile responsive
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
			name="font-size"
			label="Font size (px):"
			type="number"
			bind:value={font_size}
		/>
		<Input name="background" label="Background:" bind:value={background} />
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
		--background:{background}; 
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
		background: var(--background);

		color: var(--text-color);
		font-size: var(--font-size);
		font-weight: var(--font-weight);

		width: 600px; /* Scale x2 at build time */
		height: 315px; /* Scale x2 at build time */

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
		display: flex;
		gap: 6rem;
		width: fit-content;
		margin: 0 auto;
	}
</style>
