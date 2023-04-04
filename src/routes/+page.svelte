<script lang="ts">
	import InputField from '../components/inputField.svelte';
</script>

<main>
	<form action="">
		<InputField label="Day" placeholder="DD" />
		<InputField label="Month" placeholder="MM" />
		<InputField label="Year" placeholder="YYYY" />

		<button type="submit" class="btn-submit" />
	</form>

	<h2><span class="value">--</span>years</h2>
	<h2><span class="value">--</span>months</h2>
	<h2><span class="value">--</span>days</h2>
</main>

<style>
</style>
