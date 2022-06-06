<script lang="ts">
	let email = '';
	let password = '';

	const login = () => {
		console.log(email, password);
	};
	const logout = () => {
		console.log('logout');
	};
</script>

<svelte:head>
	<title>SvelteKit - Supabase Auth</title>
</svelte:head>

<form on:submit|preventDefault={login}>
	<input type="email" name="email" id="email" placeholder="email" bind:value={email} />
	<input
		type="password"
		name="password"
		id="password"
		placeholder="password"
		bind:value={password}
	/>
	<button type="submit">Login</button>
</form>

<button on:click={logout}>Logout</button>
