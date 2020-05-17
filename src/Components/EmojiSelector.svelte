<script>
  import data from "./data.js";
  import Emoji from "./Emoji.svelte";
  import ThemeCreator from "./ThemeCreator.svelte";
  import Previewer from "./Previewer.svelte";

  let emojis = data.data["emojis"];
  let selectedId;
  $: selectedIds = [];

  function handleMessage(e) {
    let content = { text: `${e.detail.id}` };
    selectedIds = selectedIds.concat(content);
  }

  export let selectedTheme;
  export let fontSize;
  export let maxFontSizeRem = 48;
</script>

<style>
  .theme-wrapper {
    float: left;
    position: relative;
  }
  .selector-wrapper {
    display: inline-block;
    overflow: auto;
/*     min-height: 400px;
    max-height: 50%;
    min-width: 400px;
    max-width: 50%; */
  }
</style>

<h1>Emoji Selector</h1>

<div class="theme-wrapper">
  <ThemeCreator bind:selectedTheme bind:fontSize {maxFontSizeRem} />
  <Previewer {selectedTheme} {fontSize} id={selectedId} {maxFontSizeRem} />
</div>

<div class="selector-wrapper d-flex justify-content-between flex-wrap">
  {#each emojis as { Hex, Dec }, i}
    <Emoji
      hexValue={`0x${Hex}`}
      id={i}
      bind:selectedId
      on:message={handleMessage} />
  {/each}
</div>

<div class="selected-wrapper d-flex justify-content-start flex-wrap">
  {#each selectedIds as { text }, i}
    <pre>{i + 1}) {text}{'\t'}</pre>
  {/each}
</div>
