<script lang="ts">
	import { PUBLIC_API_URL } from '$env/static/public';
	import Card from './Card.svelte';
	import { io } from 'socket.io-client';

	let selected: number[] = []
	let cards: string[] = []

	const socket = io(PUBLIC_API_URL);

	socket.on("new_cards_set", (new_cards) => {
		console.log(new_cards)
		cards = new_cards
	})

	const clickHandler = (card: number) => {
		selected = selected.includes(card)
				? [...selected.filter((e) => e !== card)]
				: [card, ...selected]

		if (selected.length === 3) {
			socket.emit("reply", selected);
		}

		if (selected.length >= 3) {
			selected = []
		}
	}

</script>

<svelte:head>
	<title>Set Cards</title>
	<meta name="description" content="Set! Set!" />
</svelte:head>

<section>
	{#each cards as card, i}
		<Card
				index={i}
				color={card[0]}
				pattern={card[1]}
				filled={card[2]}
				number={card[3]}
				selected={selected.includes(i)}
				on:click={() => clickHandler(i)}
				on:keypress={() => clickHandler(i)}
		/>
	{/each}
</section>

<style>
	section {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-template-rows: repeat(3, 1fr);
		gap: 3%;
		max-width: 95vw;
		max-height: 90vh;
	}
</style>
