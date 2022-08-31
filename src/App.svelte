<script>
import Loading from "./components/Loading.svelte"
import Login from "./components/Login.svelte"
import Todo from "./components/Todo.svelte"

	let userObj = null
	const userbase = window.userbase
	let authP = userbase.init({appId: '88e45c16-1ce7-47bd-aede-a9deb8acab96'}).then(({user}) => userObj = user)
	let username, password, errMsg

	const signIn = (e) => authP = userbase.signIn({username: e.detail.username, password: e.detail.password}).then(user => userObj = user).catch(err => errMsg = err)
	// const signUp = () => authP = userbase.signUp({username, password}).then(user => userObj = user)
	const signOut = () => authP = userbase.signOut({username, password}).then(user => userObj = null)
	
	let todos = [], newTodo, todoP
	const databaseName = 'todos'

	function changeHandler(items){todos = items}

	$: if(userObj) todoP = userbase.openDatabase({databaseName, changeHandler})

	function addTodo(e){
		todoP = userbase.insertItem({databaseName, item: e.detail.newTodo})
		newTodo = ''
	}

	function deleteTodo(e){
		todoP = userbase.deleteItem({databaseName, itemId: e.detail.id})
	}
</script>

<main>
		{#await authP}

			<Loading />

		{:then _}

			{#if !userObj}

				<Login username={username} password={password} on:signIn = {signIn} errMsg={errMsg}/>

			{:else}

				<Todo userObj={userObj} todoP={todoP} newTodo={newTodo} todos={todos} on:signOut={signOut} on:addTodo={addTodo} on:deleteTodo={deleteTodo}/>
				
			{/if}

		{:catch error} Error! {error}

		{/await}
</main>

<style>
	
</style>