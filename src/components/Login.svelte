<script>
    import {createEventDispatcher} from 'svelte'
    export let username, password, errMsg
    const dispatch = createEventDispatcher()

    function signIn(){
        dispatch('signIn', {username, password})
    }
</script>

<div class="row">
    <div class="col-4"></div>
    <div class="col-4">
        <form class="card bg-secondary">
            <h1 class="card-header text-center text-white">Login / Register</h1>
            <div class="card-body p-5">
                <label class="h4 text-white" for="username">Username</label>
                <input class="form-control mb-3" type="text" bind:value={username}>
                <label class="h4 text-white" for="password">Password</label>
                <input class="form-control mb-3" type="password" bind:value={password}>
                {#if errMsg}<span class="text-danger">{errMsg}</span>{/if}
            </div>
            <div class="card-footer row">
                <div class="col-2"></div>
                <button class="col-4 btn btn-primary mx-2" on:click={signIn}>Login</button>
                <!-- <button class="col-4 btn btn-primary mx-2" on:click={signUp}>Register</button> -->
                <div class="col-2"></div>
            </div>
        </form>
    </div>
    <div class="col-4"></div>
</div>

<style>

</style>