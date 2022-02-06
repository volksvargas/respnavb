

<script context="module">
    export async function preload(page, session) {
        const { query } = page.query
        return { query }
    }
</script>

<script>
    export let query
</script>


<section>
    <h1>Search: "{query}"</h1>
</section>
