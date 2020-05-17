<script>
  export let value = 16;
  export let maxFontSizeRem = 32;
</script>

<style>
  input {
    margin: 0.4rem;
  }
  div {
    display: inline;
  }
</style>

<div>
  Font size
  <input
    type="range"
    id="size"
    name="size"
    min="0"
    max={maxFontSizeRem}
    step={0.25}
    bind:value />
  {value} rem ({value * 16} px)
</div>
