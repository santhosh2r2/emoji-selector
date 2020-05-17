<script>
  import { data } from "./data.js";
  let themes = data.themes;

  export let selectedTheme;
  function handleClick(id) {
    selectedTheme = id;
  }
</script>

<style>
  div {
    margin: 2rem 0;
  }
  button {
    margin: 0 0.5rem;
  }
</style>

<div>
  <div class="btn-group" role="group" aria-label="Basic example">
    {#each themes as { Name }, i}
      <button
        type="button"
        class="btn btn-secondary"
        on:click={() => handleClick(i)}>
        {Name}
      </button>
    {/each}
  </div>
</div>
