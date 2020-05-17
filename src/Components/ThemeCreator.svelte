<script>
  /* 
Hex         Dec       Name
0x1F3FF     &#127999; Dark 
0x1F3FE     &#127998; Medium Dark
0x1F3FD     &#127997; Medium
0x1F3FC     &#127996; Medium Light
0x1F3FB     &#127995; Light 
*/

  import Themes from "./Themes.svelte";
  import FontSelector from "./FontSelector.svelte";
  export let selectedTheme;
  export let fontSize;
  export let maxFontSizeRem;
</script>

<style>
  div {
    display: inline-block;
  }
</style>

<div>
  <Themes bind:selectedTheme />
  <FontSelector bind:value={fontSize} {maxFontSizeRem} />
</div>
