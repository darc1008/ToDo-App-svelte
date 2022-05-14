<script>
    import {supabase} from '../supabaseClient'
    let loading=false
    let email
    const handleLogin = async()=> {
        try{
            loading=true
            const { error } = await supabase.auth.signIn({email})
            if(error) throw error 
            alert('check your email for the loginh link!')
        }catch(error){
            alert(error.error_description || error.message)
        } finally {
            loading=false
        }
    }
</script>
<form class="row flex flex-center" on:submit|preventDefault={handleLogin}>
    <div>
        <h1>Armonik To-Do</h1>
        <p>SIng in via magic link whit your email</p>
        <div>
            <input
            class="inputField" 
            type="email"
            placeholder="Your Email"
            bind:value={email}>
        </div>
        <div>
            <input type="submit" value={loading ? "Loading":"Send Maginc Link"} disabled={loading}>
        </div>
    </div>
</form>
