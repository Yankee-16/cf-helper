<script>
	import { MaterialApp, TextField, Button, Card, ProgressCircular, ListItemGroup, ListItem } from 'svelte-materialify';
	import axios from 'axios'

	let handle = ''

	let loading = false
	let loaded = false

	let error = ''

	let user = {

	}

	const handleSubmit = async() => {
		let url = `https://codeforces.com/api/user.info?handles=${handle}`
		loading = true
		loaded = false
		console.log(url)
		const res = await axios.get(url)

		console.log(res)

		user = res.data["result"][0]

		loading = false
		loaded = true
	}
</script>

<link href="https://unpkg.com/tailwindcss@^2/dist/tailwind.min.css" rel="stylesheet">

<MaterialApp >
<main>
	
		<h1>Codeforces Helper</h1>
	
		<p class="font-serif w-auto md:w-2/3 m-auto leading-24px">Codeforces Helper will recommend problems that will help the user to improve their perfomance in Codeforces. It recommends problems depending on the users recent stats. Insert your Codeforces handle and press go to get started...</p>
		

		<div class="w-8/10 md:w-2/5 m-auto mt-3">

			<TextField color="secondary" bind:value={handle}>
				Codeforces handle
			</TextField>
		</div>


		<Button class="primary-color" on:click={handleSubmit}>Submit</Button>


		<div class="my-3 m-auto">

			{#if loading}
			<ProgressCircular size={50} indeterminate color="indigo" />
			
			{:else if loaded === true }
	
			<Card shaped raised style="max-width: 40%;" class="m-auto">
				<div class="px-4 py-3">
					<ListItemGroup>
						<ListItem><span style="color: #ff3e00">Name:</span> {user.firstName} {user.lastName} </ListItem>
						<ListItem><span style="color: #ff3e00">Max rating:</span> {user.maxRating} </ListItem>
					</ListItemGroup>
				</div>
			</Card>
			{/if}
		</div>


	</main>
</MaterialApp>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4rem;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>