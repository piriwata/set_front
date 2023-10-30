<script lang="ts">
  import { fly } from 'svelte/transition';

  export let player_id: string
  export let score: number
  export let total: number
</script>

<div class="score_board">
  <div class="name">
      {player_id.slice(0, 8)}
  </div>
  <div class="score">
    {#key score}
      <span in:fly class="score">
        {score ?? 0}
      </span>
    {/key}
    /
    <span class="total">
      {total ?? 0}
    </span>
  </div>
</div>

<style>
  div.score_board {
      width: auto;
  }
  div.name {
      font-size: 1rem;
      padding: 0.3rem;
  }
  div.score {
      text-align: center;
      background-color: aliceblue;
      padding: 0.2rem 0.4rem;
      font-size: 1.5rem;
      border: solid 2px #6091d3;
      border-radius: 6px;
  }
  span.score {
      vertical-align:20%;
  }
  span.total {
      vertical-align:-20%;
  }
</style>
