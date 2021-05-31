<script>
  import Search from './Search.svelte'
  let usernameInputField = '';
  let repositories = undefined;

  async function onSubmit() {
  	const url = `https://api.github.com/users/${usernameInputField}/repos`;

  	const response = await fetch(url);
  	repositories = await response.json();
  	console.log('loaded repositories', repositories)
  }
</script>

<main>
	<form on:submit|preventDefault={onSubmit}>
		<lable for="username">Enter a GitHub username:</lable>
		<input type="text" name="username" placeholder="jackfranklin" bind:value={usernameInputField}/>
		<button type="submit">Load repositories</button>
	</form>
	{#if repositories}
		<Search {repositories} />
	{/if}
</main>

<style>
	main {
		width: 80%;
		max-width: 800px;
		margin: 20px auto;
		padding: 20px;
	}

	label {
		font-weight: bold;
	}

	input {
		width: 80%;
	}

</style>