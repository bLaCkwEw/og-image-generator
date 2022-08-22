<script>
	export let name,
		label,
		type = "text",
		value;
</script>

{#if type === "text"}
	<div class="input">
		<label for={name}>{label}</label>
		<input type="text" {name} bind:value />
	</div>
{/if}

{#if type === "number"}
	<div class="input">
		<label for={name}>{label}</label>
		<input type="number" {name} bind:value />
	</div>
{/if}

{#if type === "color"}
	<div class="input">
		<label for={name}>{label}</label>
		<input type="color" {name} bind:value />
	</div>
{/if}

<style>
	.input {
		display: flex;
		flex-direction: column;
	}
</style>
