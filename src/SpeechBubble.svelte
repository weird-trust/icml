<script>
  export let onClose;
  export let onShowAbout;
  export let onShowPopupLinks;
  export let onShowArtistInfo;
  export let onShowClippyInfo;
</script>

<div class="speech-bubble">
  <div class="speech-bubble-content">
    <p>How can I help you with my skills today?</p>
    <ul>
      <li>
        <button on:click={onShowPopupLinks}
          >1. On which platforms can I listen to or buy the album?</button
        >
      </li>
      <li>
        <button on:click={onShowArtistInfo}
          >2. Where can I find more about the artist?</button
        >
      </li>
      <li><button on:click={onShowAbout}>3. Why this page?</button></li>
      <li>
        <button on:click={onShowClippyInfo}
          >4. What are you doing here, Clippy?</button
        >
      </li>
    </ul>
    <slot></slot>
    <button class="close-button" on:click={onClose}>Close</button>
  </div>
  <div class="speech-bubble-arrow"></div>
</div>

<style>
  .speech-bubble {
    position: absolute;
    bottom: 120px; /* Positioniere die Sprechblase über Clippy */
    right: 20px; /* Positioniere die Sprechblase neben Clippy */
    width: 300px;
    background: #fff;
    border: 2px solid #000;
    border-radius: 10px;
    box-shadow: 5px 5px 0 #00000067;
    z-index: 1002; /* Stelle sicher, dass die Sprechblase über anderen Elementen liegt */
  }
  @media (max-width: 768px) {
    .speech-bubble {
      top: 110px;
      bottom: auto;
      right: 20px;
    }

    .speech-bubble-arrow {
      position: absolute;
      top: -20px;
      right: 20px;
      transform: rotate(180deg);
    }
  }

  .speech-bubble-content {
    padding: 10px;
    font-family: "Microsoft Sans Serif", sans-serif;
    font-size: 12px;
  }

  .speech-bubble-arrow {
    position: absolute;
    bottom: -20px;
    right: 20px;
    width: 0;
    height: 0;
    border-left: 20px solid transparent;
    border-right: 20px solid transparent;
    border-top: 20px solid #fff;
    border-top-color: #0000008a;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    margin-bottom: 10px;
  }

  button {
    background: none;
    border: none;
    color: #0000ee;
    text-decoration: none;
    padding: 5px;
    cursor: pointer;
    font-family: "Microsoft Sans Serif", sans-serif;
    font-size: 12px;
  }

  button:hover {
    text-decoration: underline;
  }

  .close-button {
    background: #c0c0c0;
    border: 2px solid #000;
    padding: 2px 10px;
    cursor: pointer;
    font-family: "Microsoft Sans Serif", sans-serif;
    font-size: 12px;
    margin-top: 10px;
    text-decoration: none;
    color: #000;
  }

  .close-button:active {
    box-shadow: inset 2px 2px 0 #000;
  }
</style>
