<script lang="ts">
	import Card from './Card.svelte';
	import { io } from 'socket.io-client';

	let selected: number[] = []
	let cards: string[] = [
			"RCN1", "GSB1", "BDF1", "GSF2", "BCB2", "RDN2", "BSF3", "RDN3", "GCB3", "RDB1", "BSF2", "GCN3"
	]

	const socket = io("wss://dented-gigantic-whistle.glitch.me", {
		withCredentials: true
	});

	const clickHandler = (card: number) => {
		socket.emit("reply");

		selected = selected.includes(card)
				? [...selected.filter((e) => e !== card)]
				: [card, ...selected]

		if (selected.length === 3) {
			socket.emit("answer", selected);
			cards =[
				"RCB1", "GSB1", "BDB1", "GSB2", "RCB2", "RDB2", "BSF3", "RDN3", "GCB3", "RDB1", "BSF2", "GCN3"
			]
		}

		if (selected.length >= 3) {
			selected = []
		}
	}

	socket.on("new_cards", () => {

	})
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
		max-width: 100vh;
		max-height: 90vh;
	}
</style>
