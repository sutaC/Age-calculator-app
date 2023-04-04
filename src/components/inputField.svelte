<script lang="ts">
	export let label: string = Math.random().toString();
	export let placeholder: string = label;
</script>

<div class="field">
	<label for={label}>{label}</label>
	<input type="number" name={label} id={label} {placeholder} />
	<p class="error">Error</p>
</div>

<style>
	.error {
		visibility: hidden;
	}
</style>
