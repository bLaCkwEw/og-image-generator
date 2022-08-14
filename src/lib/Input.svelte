<script>
	export let name, label, value;
</script>

<div class="input">
	<label for={name}>{label}</label>
	<input type="text" {name} bind:value />
</div>

<style>
	.input {
		display: flex;
		flex-direction: column;
	}
</style>
