<script>
	import '../app.css';
</script>

<body class="grid place-items-center h-screen">
	<slot />
</body>

<style lang="postcss">
	:global(html) {
		background-color: theme(colors.base-100);
	}
</style>
