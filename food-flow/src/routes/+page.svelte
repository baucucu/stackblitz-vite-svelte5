<script>
    import PocketBase from 'pocketbase';
    const pb = new PocketBase('https://food-flow.pockethost.io');
    async function login() {
        console.log("login");
        await pb.collection('users').authWithOAuth2({ provider: 'google' });
        console.log(pb.authStore.isValid);
        console.log(pb.authStore.token);
        console.log(pb.authStore.model.id);
    }
</script>

<h1>Welcome to SvelteKit</h1>
{#if pb.authStore.isValid}
    <h2>Logged in</h2>
    <p>Token: {pb.authStore.token}</p>
    <p>User ID: {pb.authStore.model.id}</p>
    <button on:click={() => pb.authStore.clear()}>Logout</button>
    {:else}
        <h2>Not logged in</h2>
        <button on:click={() => login()}>Login</button>
{/if}
