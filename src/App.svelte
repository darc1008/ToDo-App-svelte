<script>
	import Todos from './components/Todos.svelte'
	import Alert from './components/Alert.svelte'
	import {user} from "./stores"
	import {supabase} from './supabaseClient'
	import Auth from './components/Auth.svelte'
	import Profile from './components/Profile.svelte'
 import {todos} from './stores.js'

	user.set(supabase.auth.user())
	supabase.auth.onAuthStateChange((_, session)=>{
		user.set(session.user)
	})

	console.log(user)
</script>
{#if $user}
	<Alert />
	<Todos bind:todos={$todos} />
{:else}
	<Auth />
{/if}
