<script>
    import {onMount} from 'svelte';

    let todoItem = $state('');
    let todoList = $state([]);

    onMount(()=> {
        let storedList = localStorage.getItem("storedList");
        if (storedList) {
            todoList = (JSON.parse(storedList));
        }
    })

    function updateList() {
        return localStorage.setItem("storedList", JSON.stringify(todoList));
    }


    // Add todo item to todo list
    function addItem(event) {
        event.preventDefault();
        if (todoItem.trim().length === 0) {
            return;
        }
        todoList = [...todoList, {
            text: todoItem,
            done: false
        }];
        updateList();
        todoItem = '';
    }   
    // Remove item from todo list
    function removeItem(index) {
        todoList.splice(index,1);
        updateList();
    }

    function clearAll() {
        todoList = '';
        localStorage.clear();
    }


</script>

    <form onsubmit={addItem}>
        <input type="text" bind:value={todoItem}>
        <button class="my-buttons" type="submit">Add</button>
    </form>

    <div class="todo-list">
        <ul>
            {#each todoList as item, index}
            <li>
                <input type="checkbox" bind:checked={item.done} onChange={updateList()}>
                <span class:done={item.done}>{item.text}</span>
                <button class="my-buttons" type="button" onclick={() => removeItem(index)}>&times;</button>
            </li>
            {/each}
        </ul>
    </div>

    {#if todoList.length > 0}
    <button class="clearAll" onclick={clearAll}>Clear All</button>
    {:else}
    <button class="clearAll" disabled>Clear All</button>
    {/if}

<style>
    :root {
        --pink: #EED0F2;
        --lightRed: #FDAAAA;
        --red: #BF0B1A;
        --lavender: #CEB3F2;
        --lilac: #C9BDF2;
        --blue: #B6D6F2;
        --lightBlue: #C9EBF2;
        --Buttons: 'Alfa Slab One', system-ui;
        --text: 'Baloo 2 Variable', system-ui;
        --titles: 'Calistoga', system-ui;
    }

    ul{
        list-style: none;
        color: black;
        font-family: var(--text);
    }
    input[type="text"] {
        background-color: var(--blue);
        border: 2.5px black outset;
        border-radius: 5px;
        font-family: var(--text);
    }
    input[type="checkbox"]{
        height: 20px;
        width: 20px;
        accent-color: var(--lightBlue);
    }
    li span.done {
        text-decoration: line-through;
        color: var(--lilac);
    }
    :global(body) {
    background-color: var(--pink);
    margin: 6vw 44vw;
    }
    button {
        background-color: var(--blue);
        font-family: var(--Buttons);
        border-radius: 5px;
        transition: transform 0.3s ease-in-out;
        transition: background-color 0.3s ease;
    }
    .my-buttons:hover {
        transform: scale(1.1);
        background-color: var(--lightBlue);
        }
    .clearAll {
        background-color: var(--lightRed);
        transition: transform 0.3s ease-in-out;
        transition: background-color 0.3s ease;
        
    }
    .clearAll:hover {
        transform: scale(1.1);
        background-color: var(--red);
        }
    
</style>