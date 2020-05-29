<script>
  import Navbar from "./Navbar.svelte";
  import Player from "./Player.svelte";
  import AddPlayer from "./AddPlayer.sgvelte";

  export let title;

  let players = [
    {
      name: "h4ck0r",
      score: 31415926535
    },
    {
      name: "Winner",
      score: 200
    },
    {
      name: "Nice Guy",
      score: 100
    },
    {
      name: "John",
      score: 87
    }
  ];

  const addPlayer = e => {
    const newPlayer = e.detail;
    players = sortPlayersByScore([...players, newPlayer]);
  };

  const removePlayer = e => {
    players = sortPlayersByScore(
      players.filter(player => player.name !== e.detail)
    );
  };

  const sortPlayersByScore = myPlayers =>
    myPlayers.sort((a, b) => b.score - a.score);
</script>

<div class="container">
  <Navbar {title} />
  <AddPlayer on:addplayer={addPlayer} />
  {#if players.length === 0}
    <p>No Players!</p>
  {:else}
    {#each players as player}
      <Player
        name={player.name}
        score={player.score}
        on:deleteplayer={removePlayer} />
    {/each}
  {/if}
</div>
