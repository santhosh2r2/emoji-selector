<script>
  import data from "./data.js";
  import Emoji from "./Emoji.svelte";
  let emojis = [];
  emojis = data.data["emojis"];
  let selectedId;
</script>

<style>
  .emoji-wrapper {
    display: inline-block;
    overflow: auto;
    min-height: 400px;
    max-height: 40rem;
    min-width: 400px;
    max-width: 50%;
  }
</style>

<div>
  <h1>Emoji Selector</h1>
  <div class="emoji-wrapper d-flex justify-content-between flex-wrap">
    {#each emojis as { Hex, Dec }, i}
      <Emoji hexValue={`0x${Hex}`} id={i} bind:selectedId />
    {/each}
  </div>
</div>
