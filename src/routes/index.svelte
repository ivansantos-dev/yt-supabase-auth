<script lang="ts">
	let email = '';
	let password = '';

	const signInWithMagicLink = () => {
		console.log(email);
	};
	const signOut = () => {
		console.log('logout');
	};
</script>

<svelte:head>
	<title>SvelteKit - Supabase Auth</title>
</svelte:head>

<form on:submit|preventDefault={signInWithMagicLink}>
	<input type="email" name="email" id="email" placeholder="email" bind:value={email} />
	<button type="submit">Sign In with Magic Link</button>
</form>

<button on:click={signOut}>Sign Out</button>
