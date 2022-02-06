
<script>
    export let segment
    export let showSide
    import { goto } from '@sapper/app'
    import { fly, fade } from 'svelte/transition'
    import { search_icn } from '../_libs/icons.js'

    let query
   
	$: aria = (path) => path == segment ? 'page' : undefined
    
    const closeMenu = () => setTimeout(() => { showSide = false }, 100)
    const search = () => { goto(`/search?query=${query}`); closeMenu() }
    const listen = (e) => e.target.tagName == 'A' && closeMenu()
</script>


<div transition:fade={{duration:300}} on:click={() => showSide = false}></div>

<nav on:click={listen} transition:fly={{x:300, duration:300}}>
    <form on:submit|preventDefault={search}>
        <i>{@html search_icn}</i>
        <input bind:value={query} placeholder='Search'>
    </form>
    <a href="/" rel="prefetch" aria-current={aria()}>Start</a>
    <a href="/about" rel="prefetch" aria-current={aria('about')}>About</a>
    <a href="/blog" rel="prefetch" aria-current={aria('blog')}>Blog</a>
</nav>


<style>
    div {
        position:fixed;
        top:55px;
        height: calc(100vh - 55px);
        width:100vw;
        z-index:20;
        background:rgba(0,0,0,0.5);
    }
    nav {
        position: fixed;
        right: 0;
        top:55px;
        height: calc(100vh - 55px);
        max-width: 300px;
        width: 100vw;
        z-index:30;
        background: #eee;
        overflow-y:auto;
    }
    a {
        display: block;
        padding: .8em 1.6em;
        text-align: right;
        color: #666;
        position: relative;
        text-decoration:none;
        border-bottom:1px solid var(--medium);
    }
    a:first-of-type {
        border-top:1px solid var(--medium);
    }

    a:hover, [aria-current] {
         color: var(--bright);
         background: #fff;
    }

	form {
		background:#fff;
		padding:.4em;
		border-radius:2px;
        display:flex;
		align-items: center;
        margin:1em 2em;
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
	}
	input:focus {
		outline: none;
	}
    input::placeholder { color: #aaa; }
    input:-ms-input-placeholder { color: #aaa; }
    input::-ms-input-placeholder { color: #aaa; }

    @media (max-width: 900px) {
        div, nav {
            top:45px;
        }
    }
</style>