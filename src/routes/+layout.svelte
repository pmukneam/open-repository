<nav class="header">
	<div class="left-section"><strong>Open-Repository</strong></div>
</nav>
<main>
	<slot />
</main>

<style>
	.header {
		height: 6rem;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		background-color: #232627;
		border: none;
		z-index: 100;
	}

	main {
		padding-top: 5rem;
	}

	:golbal(body) {
		margin: 0;
	}

	.left-section {
		color: white;
		display: flex;
		align-items: center;
	}
</style>
