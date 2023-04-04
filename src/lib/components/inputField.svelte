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
	* {
		margin: 0;
		padding: 0;
	}

	div > * {
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

	.error {
		visibility: hidden;
	}
</style>
