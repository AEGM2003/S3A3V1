<script>
    import ToDo from './ToDo.svelte';
</script>

<h1>&#9753 My Gift List</h1>
<style>
    :root {
         --titles: 'Calistoga', system-ui;
         --lavender: #CEB3F2;

    }
    h1{
        font-family: var(--titles);
        padding: 0.2vw;
        background-color: var(--lavender);
        border: black 2.5px outset;
        border-radius: 5px;
    }
</style>
<ToDo />