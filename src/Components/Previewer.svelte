<script>
  import { data } from "./data.js";
  let emojis = data.emojis;
  let themes = data.themes;

  export let fontSize = 1;
  export let selectedTheme = 0;
  export let id = 0;
  export let maxFontSizeRem = 32;

  $: fontSizeRem = fontSize;
  $: themeNone = selectedTheme === 0;

  $: content = () => {
    let emoji = emojis[id];
    let theme = themes[selectedTheme];
    let emojiText = String.fromCodePoint(`0x${emoji.Hex}`);
    let themeText = "";
    if (theme && selectedTheme != 0) {
      themeText = String.fromCodePoint(`0x${theme.Hex}`);
    }
    let finalText = emojiText + themeText;

    let canvas = document.getElementById("myCanvas");
    if (canvas) {
      let ctx = canvas.getContext("2d");
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.font = `${fontSizeRem * 16}px Arial`;
      ctx.fillText(finalText, (fontSizeRem * 16) / 4, fontSizeRem * 16 * 1.25);
    }
    return finalText;
  };

  function handleClick() {
    var link = document.createElement("a");
    link.download = emojis[id].Hex + ".png";
    link.href = document.getElementById("myCanvas").toDataURL();
    link.click();
  }
</script>

<style>
  .preview {
    width: 48rem;
    height: 48rem;
    text-align: center;
  }
  .canvas-hide {
    display: none;
    text-align: center;
    border: 1px solid black;
    margin: auto;
  }
  .emoji-content {
    font-size: 2rem;
    color: purple;
  }
</style>

<div>
  <!-- <p>Emoji Hex: {emojis[id].Hex}</p>
  <p>Emoji HTML: &#{emojis[id].Dec};</p>
  <br />
  <p>Theme Hex: {themes[selectedTheme].Hex}</p>
  <p>Theme HTML: &#{themes[selectedTheme].Dec};</p>
  <br /> -->
  <p class="emoji-content">
    HTML:
    <strong>&#{emojis[id].Dec};</strong>
    {#if !themeNone}
      <strong>&#{themes[selectedTheme].Dec};</strong>
    {/if}
  </p>
</div>
<div class="preview">
  <button class="btn btn-primary" on:click={handleClick}>
    Download as PNG
  </button>
  <p style="font-size: {fontSizeRem}rem;">{content()}</p>
  <canvas
    class="canvas-hide"
    width="{maxFontSizeRem * 16 * 2}px"
    height="{maxFontSizeRem * 16 * 2}px"
    id="myCanvas" />

</div>
