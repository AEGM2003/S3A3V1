<script>
    import ToDo from './ToDo.svelte';
</script>

<h1>My Gift List App</h1>
<style>
    :root {
         --titles: 'Calistoga', system-ui;
         --lavender: #CEB3F2;

    }
    h1{
        font-family: var(--titles);
        padding: 0.2vw;
        background-color: var(--lavender);
        border-radius: 5px;
    }
</style>
<ToDo />