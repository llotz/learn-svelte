<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let name = "John";
  export let score = 100;
  let showControls = false;

  const toggleControls = () => (showControls = !showControls);
  const addPoints = () => (score += 1);
  const removePoints = () => (score -= 1);
</script>

<style>

</style>

<div class="card">
  <h1>
    {name}
    <button on:click={toggleControls} class="btn btn-secondary">
      {#if showControls}-{:else}+{/if}
    </button>
    <button
      class="btn btn-danger"
      on:click={() => dispatch('deleteplayer', name)}>
      X
    </button>
  </h1>
  <h3>Score: {score}</h3>
  {#if showControls}
    <button type="button" class="btn" on:click={addPoints}>+1</button>
    <button type="button" class="btn btn-dark" on:click={removePoints}>
      -1
    </button>
    <input type="number" bind:value={score} />
  {/if}
</div>
