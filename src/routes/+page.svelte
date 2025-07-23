<script lang="ts">
	import { authClient } from '$lib/auth-client';
  import useFetcher from '$lib/use-fetcher.svelte';

	function signIn() {
		authClient.signIn.social({
			provider: 'linkedin'
		});
	}

	function signOut() {
		authClient.signOut();
	}

  const currentSession = authClient.useSession();
	const lastUsedSocial = useFetcher(() => authClient.lastUsedSocialProvider());
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>

<button onclick={signIn}> Sign In with LinkedIn </button>
<button onclick={signOut}> Sign Out </button>

<div>
  {#if lastUsedSocial.isLoading}
	  <p>Fetching last used social...</p>
  {:else if lastUsedSocial.error}
	  <pre>{JSON.stringify(lastUsedSocial.error, null, 2)}</pre>
  {:else if lastUsedSocial.data?.data}
  	<h3>Last Used Social</h3>
  	<p>{lastUsedSocial.data.data}</p>
  {:else if lastUsedSocial.data?.error}
  	<h3>Last Used Social Error</h3>
	  <pre>{JSON.stringify(lastUsedSocial.data.error, null, 2)}</pre>
  {/if}
</div>

<h1>Current Session</h1>

<div>
  {#if $currentSession.data}
    <div class="session-container">
      <div class="session-flex">
        <div class="session-column">
          <h3>Session</h3>
          <pre class="json-block">{JSON.stringify($currentSession.data.session, null, 2)}</pre>
        </div>
        <div class="session-column">
          <h3>User</h3>
          <pre class="json-block">{JSON.stringify($currentSession.data.user, null, 2)}</pre>
        </div>
      </div>
    </div>
  {:else}
    <p>No current session</p>
  {/if}
</div>
