<script>
  import { onMount, onDestroy } from "svelte";

  export let onClose;
  let popup;
  let offsetX = 0;
  let offsetY = 0;
  let isDragging = false;
  let animationFrame;

  let posX = 100;
  let posY = 100;
  let speedX = 0.5;
  let speedY = 0.5;

  function handleMouseDown(event) {
    isDragging = true;
    offsetX = event.clientX - popup.getBoundingClientRect().left;
    offsetY = event.clientY - popup.getBoundingClientRect().top;
    document.addEventListener("mousemove", handleMouseMove);
    document.addEventListener("mouseup", handleMouseUp);
    cancelAnimationFrame(animationFrame);
  }

  function handleTouchStart(event) {
    isDragging = true;
    const touch = event.touches[0];
    offsetX = touch.clientX - popup.getBoundingClientRect().left;
    offsetY = touch.clientY - popup.getBoundingClientRect().top;
    document.addEventListener("touchmove", handleTouchMove);
    document.addEventListener("touchend", handleTouchEnd);
    cancelAnimationFrame(animationFrame);
  }

  function handleMouseMove(event) {
    if (isDragging) {
      posX = event.clientX - offsetX;
      posY = event.clientY - offsetY;
      updatePopupPosition();
    }
  }

  function handleTouchMove(event) {
    if (isDragging) {
      const touch = event.touches[0];
      posX = touch.clientX - offsetX;
      posY = touch.clientY - offsetY;
      updatePopupPosition();
    }
  }

  function handleMouseUp() {
    isDragging = false;
    document.removeEventListener("mousemove", handleMouseMove);
    document.removeEventListener("mouseup", handleMouseUp);
    requestAnimationFrame(animate);
  }

  function handleTouchEnd() {
    isDragging = false;
    document.removeEventListener("touchmove", handleTouchMove);
    document.removeEventListener("touchend", handleTouchEnd);
    requestAnimationFrame(animate);
  }

  function updatePopupPosition() {
    popup.style.left = `${posX}px`;
    popup.style.top = `${posY}px`;
  }

  function animate() {
    if (!isDragging) {
      posX += speedX;
      posY += speedY;

      if (posX <= 0 || posX + popup.offsetWidth >= window.innerWidth) {
        speedX = -speedX;
      }

      if (posY <= 0 || posY + popup.offsetHeight >= window.innerHeight) {
        speedY = -speedY;
      }

      updatePopupPosition();
      animationFrame = requestAnimationFrame(animate);
    }
  }

  onMount(() => {
    updatePopupPosition();
    requestAnimationFrame(animate);
  });

  onDestroy(() => {
    cancelAnimationFrame(animationFrame);
  });

  function handleDownloadClick() {
    window.location.href = "https://institutut.bandcamp.com/";
    onClose();
  }
</script>

<div class="popup" bind:this={popup}>
  <div class="window" style="width: 90%; max-width: 300px;">
    <div
      class="title-bar"
      role="button"
      tabindex="0"
      on:mousedown={handleMouseDown}
      on:touchstart={handleTouchStart}
    >
      <div class="title-bar-text">🏴‍☠️ 🏴‍☠️ 🏴‍☠️ Pirate Bay 🏴‍☠️ 🏴‍☠️ 🏴‍☠️</div>

      <div class="title-bar-controls">
        <button aria-label="Close" on:click={onClose}></button>
      </div>
    </div>
    <div class="window-body">
      <p>You want to pirate this album? Come and get me!</p>
      <button class="button" on:click={handleDownloadClick}>Download</button>
    </div>
  </div>
</div>

<style>
  .popup {
    position: absolute;
    z-index: 1; /* Stelle sicher, dass das Popup hinter dem Player liegt */
  }

  .window {
    border: 2px solid #000;
    background: #c0c0c0;
    box-shadow: 5px 5px 0 #00000067;
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
    cursor: move; /* Zeige an, dass das Fenster verschoben werden kann */
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
