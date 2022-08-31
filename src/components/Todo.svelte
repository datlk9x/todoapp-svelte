<script>
    import {createEventDispatcher} from 'svelte'

    export let userObj, todoP, newTodo, todos
    const dispatch = createEventDispatcher()

    function signOut(){
        dispatch('signOut')
    }
    function addTodo(){
        dispatch('addTodo', {newTodo})
    }
    function deleteTodo(id){
        dispatch('deleteTodo', {id})
    }

</script>

<main>
    <h1>Hi, {userObj.username}!</h1>
    <button on:click={signOut} style="position: absolute; top: 10px; right: 10px;">Sign out</button>

    {#await todoP}

        Loading ...

    {:then _}
        
        <label for="newtodo">New Todo</label>
        <input type="text" placeholder="New todo ..." bind:value={newTodo}>
        <button on:click={addTodo}>New Todo</button>

        {#each todos as {item, itemId}, index}
            <ul>
                <li class="row">
                    <span class="col-11">{item}</span>
                    <button on:click={() => deleteTodo(itemId)} class="col-1">X</button>
                </li>
            </ul>
        {/each}

    {:catch error} Error! {error}

    {/await}
</main>

<style>

</style>