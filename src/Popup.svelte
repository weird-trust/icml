<script>
  import { onMount, onDestroy } from "svelte";

  export let onClose;
  let emojiInterval;
  let emojiIndex = 0;

  const emojis = ["🌐", "➡️", "💻", "➡️", "🔄", "➡️", "🌍"];

  function updateEmojis() {
    emojiIndex = (emojiIndex + 1) % emojis.length;
    const titleBarText = document.querySelector(".title-bar-text");
    titleBarText.innerHTML = emojis
      .slice(emojiIndex)
      .concat(emojis.slice(0, emojiIndex))
      .join(" ");
  }

  onMount(() => {
    emojiInterval = setInterval(updateEmojis, 500); // Wechsle die Emojis alle 500ms
  });

  onDestroy(() => {
    clearInterval(emojiInterval);
  });
</script>

<div class="popup">
  <div class="window" style="width: 300px;">
    <div class="title-bar">
      <div class="title-bar-text">🌐 ➡️ 💻 ➡️ 🔄 ➡️ 🌍</div>
      <div class="title-bar-controls">
        <button aria-label="Close" on:click={onClose}></button>
      </div>
    </div>
    <div class="window-body">
      <p>Internet changed my Life</p>
      <button class="button" on:click={onClose}>Click Me</button>
    </div>
  </div>
</div>

<style>
  .popup {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgb(14, 110, 110);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }

  .window {
    border: 2px solid #000;
    background: #c0c0c0;
    box-shadow: 5px 5px 0 #0000007a;
  }

  .title-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #000080;
    color: #fff;
    padding: 2px 5px;
    font-family: "Microsoft Sans Serif", sans-serif;
    font-size: 12px;
  }

  .title-bar-text {
    font-weight: bold;
    white-space: nowrap; /* Verhindert das Umbrechen der Emojis */
    overflow: hidden; /* Versteckt den Überlauf */
  }

  .title-bar-controls button {
    background: #c0c0c0;
    border: none;
    width: 16px;
    height: 16px;
    padding: 0;
    margin: 0 2px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }

  .title-bar-controls button::before {
    content: "×";
    font-size: 14px;
    line-height: 1;
  }

  .window-body {
    padding: 10px;
    font-family: "Microsoft Sans Serif", sans-serif;
    font-size: 12px;
  }

  .button {
    background: #c0c0c0;
    border: 2px solid #000;
    padding: 2px 10px;
    cursor: pointer;
    font-family: "Microsoft Sans Serif", sans-serif;
    font-size: 12px;
    margin-top: 10px;
  }

  .button:active {
    box-shadow: inset 2px 2px 0 #000;
  }
</style>
