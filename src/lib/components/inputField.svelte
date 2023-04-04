<script context="module" lang="ts">
	export type ErrorField = { field: string; message: string };
</script>

<script lang="ts">
	export let label: string = Math.random().toString();
	export let placeholder: string = label;
	export let error: ErrorField[] = [];

	export let value: number | undefined = undefined;
</script>

<div class="field" class:error={error.length > 0}>
	<label for={label}>{label}</label>
	<input type="number" name={label} id={label} {placeholder} bind:value />
	{#each error as err}
		<p class="error-message">{err.message}</p>
	{/each}
</div>

<style>
	* {
		margin: 0;
		padding: 0;
	}

	.field {
		max-width: 4rem;
	}

	.field > * {
		display: block;
		width: 100%;
	}

	label {
		font-size: 0.4rem;
		color: var(--clr-Smokey-grey);
		text-transform: uppercase;
		letter-spacing: 0.05rem;
	}

	input {
		box-sizing: border-box;

		margin: 0.1rem 0;
		padding: 0.4rem 0.2rem;

		border: 1px solid var(--clr-Smokey-grey);
		border-radius: 5px;

		font-family: 'Poppins', sans-serif;
		font-size: 0.6rem;
	}

	input::-webkit-outer-spin-button,
	input::-webkit-inner-spin-button {
		-webkit-appearance: none;
	}

	input:focus {
		outline: 1px solid var(--clr-Purple);
		caret-color: var(--clr-Purple);
	}

	.error-message {
		visibility: hidden;

		font-size: 0.35rem;
		font-weight: 400;
		font-style: italic;
	}

	.error label,
	.error-message {
		color: var(--clr-Light-red);
	}

	.error input {
		border-color: var(--clr-Light-red);
	}

	.error .error-message {
		visibility: visible;
	}
</style>
