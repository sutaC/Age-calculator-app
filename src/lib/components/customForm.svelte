<form action="">
	<slot />

	<button type="submit" />
</form>

<style>
	form {
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 1rem;

		box-sizing: border-box;
		margin-bottom: 1rem;
		padding: 0.5rem;

		position: relative;

		border-bottom: 1px solid var(--clr-Light-grey);
	}

	button {
		position: absolute;
		bottom: 0;

		transform: translate(0, 50%);

		border: none;
		border-radius: 100%;

		--btn-size: 2rem;

		width: var(--btn-size);
		height: var(--btn-size);

		background-color: var(--clr-Purple);
		background-image: url('$lib/images/icon-arrow.svg');
		background-repeat: no-repeat;
		background-position: center;
		background-size: 1rem;
	}
	button:active {
		background-color: var(--clr-Off-black);
	}
</style>
