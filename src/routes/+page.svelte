<script lang="ts">
	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';

	import InputField from '$lib/components/inputField.svelte';
	import CustomForm from '$lib/components/customForm.svelte';

	import type { ErrorField } from '$lib/components/inputField.svelte';

	let day: number | undefined;
	let month: number | undefined;
	let year: number | undefined;

	let daysFrom: number | undefined = undefined;
	let monthsFrom: number | undefined = undefined;
	let yearsFrom: number | undefined = undefined;

	let daysTweened: any;
	let monthsTweened: any;
	let yearsTweened: any;

	let errors: ErrorField[] = [];

	const handleSubmit = (e: SubmitEvent): void => {
		errors = [];
		daysFrom = undefined;
		monthsFrom = undefined;
		yearsFrom = undefined;

		// Validation

		if (!day) {
			errors = [...errors, { field: 'day', message: 'This field is required' }];
		} else if (day < 1 || 31 < day) {
			errors = [...errors, { field: 'day', message: 'Must be valid day' }];
		}

		if (!month) {
			errors = [...errors, { field: 'month', message: 'This field is required' }];
		} else if (month < 1 || 12 < month) {
			errors = [...errors, { field: 'month', message: 'Must be valid month' }];
		}

		if (!year) {
			errors = [...errors, { field: 'year', message: 'This field is required' }];
		} else if (year > new Date().getFullYear()) {
			errors = [...errors, { field: 'year', message: 'Must be in the past' }];
		}

		if (year && month && day) {
			if (day > new Date(year, month, 0).getDate()) {
				errors = [...errors, { field: 'day', message: 'Must be valid date' }];
				errors = [...errors, { field: 'month', message: '' }];
				errors = [...errors, { field: 'year', message: '' }];
			}

			// Setting values

			if (errors.length === 0) {
				const then: Date = new Date(year, month, day);
				const now: Date = new Date();

				// Calculate time

				const diffInMilliseconds = Math.abs(now.getTime() - then.getTime());
				const diffInDays = Math.floor(diffInMilliseconds / (1000 * 60 * 60 * 24));

				yearsFrom = Math.floor(diffInDays / 365);
				monthsFrom = Math.floor((diffInDays % 365) / 30);
				daysFrom = Math.floor(diffInDays % 30);

				// Animate the values

				yearsTweened = tweened(0, { duration: 700, easing: cubicOut });
				monthsTweened = tweened(0, { duration: 700, easing: cubicOut });
				daysTweened = tweened(0, { duration: 700, easing: cubicOut });

				yearsTweened.set(yearsFrom);
				monthsTweened.set(monthsFrom);
				daysTweened.set(daysFrom);
			}
		}
	};
</script>

<main>
	<CustomForm on:submit={handleSubmit}>
		<InputField
			label="Day"
			placeholder="DD"
			bind:value={day}
			error={errors.filter((err) => err.field === 'day')}
		/>
		<InputField
			label="Month"
			placeholder="MM"
			bind:value={month}
			error={errors.filter((err) => err.field === 'month')}
		/>
		<InputField
			label="Year"
			placeholder="YYYY"
			bind:value={year}
			error={errors.filter((err) => err.field === 'year')}
		/>
	</CustomForm>

	<h2>
		<span class="value"
			>{yearsFrom !== undefined ? Math.floor($yearsTweened * 100) / 100 : '--'}
		</span>years
	</h2>
	<h2>
		<span class="value"
			>{monthsFrom !== undefined ? Math.floor($monthsTweened * 100) / 100 : '--'}
		</span>months
	</h2>
	<h2>
		<span class="value"
			>{daysFrom !== undefined ? Math.floor($daysTweened * 100) / 100 : '--'}
		</span>days
	</h2>
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
		padding: 0.3rem;

		background-color: var(--clr-Off-white);
	}

	/* Main styles */

	main {
		max-width: 16rem;

		padding: 0.5rem;

		border-radius: 0.5rem;
		border-bottom-right-radius: 4rem;

		background-color: var(--clr-White);

		flex: 1;
	}

	h2 {
		margin: 0 0.5rem;

		font-size: 1rem;
		font-weight: 700;
		font-style: italic;
	}

	.value {
		font-weight: 800;
		color: var(--clr-Purple);
		margin: 0.3rem;
	}

	@media (min-width: 450px) {
		h2 {
			font-size: 2rem;
		}
	}
</style>
