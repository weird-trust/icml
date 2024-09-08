<script>
  import { onMount, onDestroy } from "svelte";

  export let onClose;
  let gifElement;
  let posX = 100;
  let posY = 100;
  let speedX = 2;
  let speedY = 2;
  let animationFrame;

  function moveGif() {
    posX += speedX;
    posY += speedY;

    if (posX <= 0 || posX + gifElement.offsetWidth >= window.innerWidth) {
      speedX = -speedX;
    }

    if (posY <= 0 || posY + gifElement.offsetHeight >= window.innerHeight) {
      speedY = -speedY;
    }

    gifElement.style.left = `${posX}px`;
    gifElement.style.top = `${posY}px`;

    animationFrame = requestAnimationFrame(moveGif);
  }

  function handleClick() {
    cancelAnimationFrame(animationFrame);
    onClose();
  }

  onMount(() => {
    gifElement.style.position = "absolute";
    moveGif();
  });

  onDestroy(() => {
    cancelAnimationFrame(animationFrame);
  });
</script>

<div class="screensaver" on:click={handleClick}>
  <img
    src="/images/windows95.png"
    alt="Windows Screensaver"
    bind:this={gifElement}
  />
</div>

<style>
  .screensaver {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: black;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 10000;
    cursor: pointer;
  }

  .screensaver img {
    width: 100px; /* Passe die Größe des GIFs an */
    height: auto;
  }
</style>
