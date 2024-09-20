<script>
  import { onMount, onDestroy } from "svelte";

  export let onClose;
  let gifElement;
  let posX = 100;
  let posY = 100;
  let speedX = 3;
  let speedY = 3;
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

<button
  class="screensaver"
  on:click={handleClick}
  on:keydown={(e) => e.key === "Enter" && handleClick()}
  aria-label="Close screensaver"
>
  <img
    src="/images/icml_screensaver.png"
    alt="Windows Screensaver"
    class="rotating"
    bind:this={gifElement}
  />
</button>

<style>
  .screensaver {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgb(157, 157, 157);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 10000;
    cursor: pointer;
  }

  .screensaver img {
    width: 200px;
    height: auto;
  }

  @keyframes rotate {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }

  .rotating {
    animation: rotate 5s linear infinite;
  }
</style>
