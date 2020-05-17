<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let hexValue;
  export let id;
  export let selectedId;
  export let selected;

  function handleClick() {
    selected = !selected;
    selectedId = id;
    if (selected) {
      dispatch("message", {
        id: selectedId
      });
    }
  }
</script>

<style>
  .emoji {
    display: inline-block;
    padding: 0.2rem;
    font-size: 1rem;
  }
  .selected {
    color: green;
  }
</style>

{#if hexValue}
  <div class="emoji">
    <button on:click={handleClick}>
      <i class:selected class={selected && 'fas fa-check'} />
      {String.fromCodePoint(hexValue)}
    </button>
  </div>
{/if}
