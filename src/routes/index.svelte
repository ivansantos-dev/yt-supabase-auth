<script lang="ts">
	import { createClient } from '@supabase/supabase-js';
	import { onMount } from 'svelte';

	let anonKey =
		'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im50cnlqa3RkbHpweXZvZXNibHR4Iiwicm9sZSI6ImFub24iLCJpYXQiOjE2NTQ4Mjg3NDgsImV4cCI6MTk3MDQwNDc0OH0.ALSMFKaXceVhLP2B3xyAOWHyQuOiwyePQM4-Xvi7CSc';
	let url = 'https://ntryjktdlzpyvoesbltx.supabase.co';

	let user: any;
	const supabase = createClient(url, anonKey);

	console.log(supabase);
	let email = '';

	const signInWithMagicLink = async () => {
		const { user, error } = await supabase.auth.signIn({ email });
		console.log(user, error);
	};

	const signOut = () => {
		supabase.auth.signOut();
	};

	onMount(() => {
		supabase.auth.onAuthStateChange((event, session) => {
			user = session?.user;
		});
	});
</script>

<svelte:head>
	<title>SvelteKit - Supabase Auth</title>
</svelte:head>

{#if user}
	<p>Signed in as {user.email}</p>
	<button on:click={signOut}>Sign Out</button>
{:else}
	<form on:submit|preventDefault={signInWithMagicLink}>
		<input type="email" name="email" id="email" placeholder="email" bind:value={email} />
		<button type="submit">Sign In with Magic Link</button>
	</form>
{/if}
