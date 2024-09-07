<script>
  export let onClose;
</script>

<div class="popup">
  <div class="window" style="width: 300px;">
    <div class="title-bar">
      <div class="title-bar-text">Links</div>
      <div class="title-bar-controls">
        <button aria-label="Close" on:click={onClose}></button>
      </div>
    </div>
    <div class="window-body">
      <ul>
        <li><a href="https://open.spotify.com" target="_blank">Spotify</a></li>
        <li><a href="https://bandcamp.com" target="_blank">Bandcamp</a></li>
        <li><a href="https://soundcloud.com" target="_blank">SoundCloud</a></li>
        <!-- Weitere Links hier hinzufügen -->
      </ul>
      <button class="button" on:click={onClose}>Schließen</button>
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
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }

  .window {
    border: 2px solid #000;
    background: #c0c0c0;
    box-shadow: 5px 5px 0 #000;
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

  .window-body ul {
    list-style-type: none;
    padding: 0;
  }

  .window-body li {
    margin-bottom: 10px;
  }

  .window-body a {
    color: #0000ee;
    text-decoration: none;
  }

  .window-body a:hover {
    text-decoration: underline;
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
