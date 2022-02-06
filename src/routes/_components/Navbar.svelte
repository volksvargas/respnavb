
<script>
	export let segment
	import { goto } from '@sapper/app'
	import SideMenu from './SideMenu.svelte'
	import SideToggle from './SideToggle.svelte'
	import { search_icn } from '../_libs/icons.js'
	
	let query
	let showSide = false
	
	$: aria = (path) => path == segment ? 'page' : undefined
</script>


<nav>
	<a href="/" rel="prefetch" class="logo" >
		<span>RESP</span><span style="color:var(--light)">NAVB</span>
	</a>
	<section>
		<a href="/" rel="prefetch" aria-current={aria()}>Start</a>
		<a href="/about" rel="prefetch" aria-current={aria('about')}>About</a>
		<a href="/blog" rel="prefetch" aria-current={aria('blog')}>Blog</a>
	</section>
    <form on:submit|preventDefault={goto(`/search?query=${query}`)}>
		<i>{@html search_icn}</i>
        <input bind:value={query} placeholder='Search'>
    </form>
	<aside>
		<SideToggle bind:showSide/>
	</aside>
</nav>

{#if showSide}
    <SideMenu {segment} bind:showSide />
{/if}


<style>
	nav {
		display:flex;
		align-items: center;
		background:var(--dark);
		box-sizing: border-box;
		width:100%;
		z-index:999;
		padding:0 4em;
	}
	section {
		display:flex;
		align-items: center;
		flex-grow:1;
	}
	a {
		display:flex;
		align-items: center;
		height:55px;
		padding: 0 1em;
		text-decoration:none;
		color:var(--light);
		font-weight:500;
		font-size:.9em;
	}
	a:hover {
		color:#fff;
	}
	a:not(.logo)[aria-current] {
		background-color: var(--medium);
		position: relative;
		color:#fff;
	}
	a.logo {
		color:#fff;
		font-weight:800;
		font-size:1.3em;
		letter-spacing: .05em;
	}
	form {
		background:var(--medium);
		padding:.2em .4em;
		border-radius:2px;
        display:flex;
		align-items: center;
	}
	form i {
		color: var(--light);
		height: 15px;
		width: 15px;
		display:flex;
		align-items: center;
	}
	input {
		margin-left:.4em;
		border:none;
		background:none;
		font-size:.9em;
		color:#fff;
	}
	input:focus {
		outline: none;
	}
	input::placeholder { color: var(--light); }
	input:-ms-input-placeholder { color: var(--light); }
	input::-ms-input-placeholder { color: var(--light); }

	aside {
		display:none;
	}

	@media (max-width: 900px) {
        section, form {
            display: none;
        }
		nav {
			padding:0;
		}
		a {
			height:45px;
		}
		a.logo {
			font-size:1.2em;
			letter-spacing: .03em;
		}
        aside {
            display: block;
            margin-left: auto;
			margin-right:20px;
        }
	}
</style>
