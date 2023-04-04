<script lang="ts">
	import InputField from '$lib/components/inputField.svelte';
	import CustomForm from '$lib/components/customForm.svelte';
</script>

<main>
	<CustomForm>
		<InputField label="Day" placeholder="DD" />
		<InputField label="Month" placeholder="MM" />
		<InputField label="Year" placeholder="YYYY" />
	</CustomForm>

	<h2><span class="value">----</span>years</h2>
	<h2><span class="value">--</span>months</h2>
	<h2><span class="value">--</span>days</h2>
</main>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,700;1,400;1,800&display=swap');

	:root {
		/* Primary */
		--clr-Purple: hsl(259, 100%, 65%);
		--clr-Light-red: hsl(0, 100%, 67%);
		/* Neutral */
		--clr-White: hsl(0, 0%, 100%);
		--clr-Off-white: hsl(0, 0%, 94%);
		--clr-Light-grey: hsl(0, 0%, 86%);
		--clr-Smokey-grey: hsl(0, 1%, 44%);
		--clr-Off-black: hsl(0, 0%, 8%);
	}

	:global(html) {
		font-family: 'Poppins', sans-serif;
		font-size: 32px;
	}

	:global(body) {
		display: flex;
		justify-content: center;
		align-items: center;
		min-height: 100vh;

		box-sizing: border-box;
		margin: 0;
		padding: 1rem;

		background-color: var(--clr-Off-white);
	}

	/* Main styles */

	main {
		max-width: 20rem;

		padding: 0.5rem;

		border-radius: 0.5rem;
		border-bottom-right-radius: 4rem;

		background-color: var(--clr-White);
	}

	h2 {
		margin: 0 0.5rem;

		font-size: 1.6em;
		font-weight: 700;
		font-style: italic;
	}

	.value {
		font-weight: 800;
		color: var(--clr-Purple);
		margin: 0.3rem;
	}
</style>
