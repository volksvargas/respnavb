
<script>
    export let showSide
</script>


<nav class:active={showSide} on:click={() => showSide = !showSide}>
    <div></div>
</nav>


<style>
	nav {
		width: 25px;
        height: 14px;
        position:relative;
        cursor: pointer;
	}
	nav:after, nav:before, div {
		content: "";
		position: absolute;
		width: 100%;
		height: 2px;
		background-color: #fff;
		transition: all 0.4s;
		transform-origin: center;
	}
	nav:before, div {
		top: 0;
	}
	nav:after, div {
		bottom: 0;
	}
	nav:before {
		width: 66%;
	}
	nav:after {
		width: 33%;
	}
	div {
		margin: auto;
	}
	nav:hover:before, nav:hover:after,
	nav.active:before, nav.active:after, nav.active div {
		width: 100%;
	}
	nav.active:before, nav.active:after {
        top: 50%;
        transform: rotate(-45deg);
	}
	nav.active div {
        transform: rotate(45deg);
        top:2px;
	}
</style>