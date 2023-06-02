<script>
    import TrashCanOutline from "svelte-material-icons/TrashCanOutline.svelte";

    export let color = "azure";

    let todos = [
        { title: "finish Svelte tutorial", completed: false },
        { title: "build an app", completed: false },
        { title: "world domination", completed: true },
    ];
    let newTask = "";

    function addTask() {
        if (newTask.trim()) {
            todos = [...todos, { title: newTask.trim(), completed: false }];
        }
    }

    function deleteTask(index) {
        todos.splice(index, 1);
        todos = todos;
    }

    function deleteAllTasks() {
        if (confirm("Are you sure you want to delete all tasks?")) {
            todos = [];
        }
    }
    
    function toggleTask(index) {
        todos[index].completed = !todos[index].completed;
        todos = todos;
    }
</script>

<div class="addTaskWrapper">
    <button on:click={addTask}>Add</button>
    <input type="text" bind:value={newTask} placeholder="New task" />
</div>
<ul>
    {#each todos as todo, index}
        <li>
            <input type="checkbox" bind:checked={todo.completed} />
            <input
                id="todoItemInList"
                placeholder="What needs to be done?"
                bind:value={todo.title}
                disabled={todo.completed}
            />
            <button
                id="deleteButton"
                on:click={() => deleteTask(index)}
                style="display: flex;"
            >
                <TrashCanOutline {color} size="1.3em"/>
            </button>
        </li>
    {/each}
</ul>

<button on:click={deleteAllTasks}>Delete All</button>

<style>
    ul {
        padding: 0;
        list-style-type: none;
    }

    li {
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-bottom: 0.5em;
    }

    .addTaskWrapper {
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 5px;
        margin: 0;
    }

    #todoItemInList {
        flex-grow: 1;
        text-align: left;
        border-radius: 5px;
    }

    input[type="checkbox"] {
        margin-right: 0.5em;
    }

    input {
        border-radius: 5px;
    }

    #deleteButton {
        margin-left: 0.5em;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: transparent;
        border: none;
        cursor: pointer;
        padding: 0;
    }

    button {
        background-color: rgba(255, 255, 255, 0.7);
        border: 1px solid rgb(186, 189, 194);
        border-radius: 0.2rem;
        margin-right: 5px;
        margin-bottom: 7px;
        padding: 5px;
        box-sizing: border-box;
        color: #111827;
        font-size: 0.7em;
        font-weight: 200;
        text-align: center;
        text-decoration: none #d1d5db solid;
        text-decoration-thickness: auto;
        box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
        cursor: pointer;
        user-select: none;
        -webkit-user-select: none;
        touch-action: manipulation;
    }

    button:hover {
        background-color: rgb(249, 250, 251);
    }

    button:focus {
        outline: 2px solid transparent;
        outline-offset: 2px;
    }

    button:focus-visible {
        box-shadow: none;
    }
</style>
