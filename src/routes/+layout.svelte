<script>
	import './styles.css';
</script>

<div class="app">
	<main>
		<slot />
	</main>
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		margin: 1rem auto;
		box-sizing: border-box;
		justify-content: center;
		align-items: center;
	}
</style>
