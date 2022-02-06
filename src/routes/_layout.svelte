
<script>
	export let segment
	import Navbar from './_components/Navbar.svelte'
</script>


<Navbar {segment} />
<main>
	<slot></slot>
</main>


<style>
	:global(:root) {
		--dark: darkred;
		--medium: firebrick;
        --bright: crimson;
		--light: lightcoral;
	}
    :global(#sapper) {
        height:100vh;
        display:flex;
        flex-direction: column;
    }
	main {
		flex-grow: 1;
		background:#e5eaeb;
		display:flex;
		flex-direction: column;
		align-items: center;
		padding:3em 0;
	}
</style>