<script lang="ts">
	import { PUBLIC_API_URL } from '$env/static/public';
	import { io } from 'socket.io-client';

	import Card from './Card.svelte';
	import Score from './Score.svelte';

	let selected: number[] = [];
	let cards: string[] = [];
	let player = { socket_id: "Loading", score: 0};
	let opponents = [];
	$: total = Object.values(opponents).reduce((sum, num) => sum + num, 0) + (player.score ?? 0);

	const socket = io(PUBLIC_API_URL);

	socket.on("new_cards_set", (new_cards, new_scores) => {
		cards = new_cards;

		if (socket.id) {
			player = { socket_id: socket.id, score: new_scores[socket.id] };
			delete new_scores[socket.id]
		}

		opponents = new_scores
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
	<div id="header">
		<Score player_id={player.socket_id} score={player.score} total={total} />
	</div>
	{#each cards as card, i}
		<Card
				color={card[0]}
				pattern={card[1]}
				filled={card[2]}
				number={card[3]}
				selected={selected.includes(i)}
				on:click={() => clickHandler(i)}
				on:keypress={() => clickHandler(i)}
		/>
	{/each}
	<div id="footer">
		{#each Object.entries(opponents) as opponent}
			<Score player_id={opponent[0]} score={opponent[1]} total={total} />
		{/each}
	</div>
</section>

<style>
	section {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-template-rows: 6rem 1fr 1fr 1fr 6rem;
		gap: 3%;
		max-width: 95vw;
		max-height: 95vh;
	}
	#header {
		grid-column: 1/5;
		margin: 0 auto;
	}
	#footer {
		width: 80%;
		display: flex;
		justify-content: space-around;
		grid-column: 1/5;
		margin: 0 auto;
	}
</style>
