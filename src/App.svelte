<script>
  import { onMount } from "svelte";
  import WinampPlayer from "./WinampPlayer.svelte";
  import GlitchEffect from "./GlitchEffect.svelte";
  import Popup from "./Popup.svelte";
  import PopupLinks from "./PopupLinks.svelte";
  import About from "./About.svelte";
  import Impressum from "./Impressum.svelte";
  import DraggablePopup from "./DraggablePopup.svelte";

  let showPlayer = false;
  let startPlaying = false;
  let showPopupLinks = false;
  let showAbout = false;
  let showImpressum = false;
  let showDraggablePopup = true; // Initial geöffnet

  function handleClosePopup() {
    showPlayer = true;
    startPlaying = true;
  }

  function handleGifClick() {
    showPopupLinks = true;
  }

  function handleClosePopupLinks() {
    showPopupLinks = false;
  }

  function handleShowAbout() {
    showAbout = true;
  }

  function handleCloseAbout() {
    showAbout = false;
  }

  function handleShowImpressum() {
    showImpressum = true;
  }

  function handleCloseImpressum() {
    showImpressum = false;
  }

  function handleCloseDraggablePopup() {
    showDraggablePopup = false;
  }
</script>

<main>
  {#if !showPlayer}
    <Popup onClose={handleClosePopup} />
  {/if}
  {#if showPlayer}
    <GlitchEffect />
    <WinampPlayer {startPlaying} />
    <div class="footer-links">
      <button class="footer-link" on:click={handleShowAbout}>
        <img src="/images/about.gif" alt="About" class="footer-gif" />
        <div>About</div>
      </button>
      <button class="footer-link" on:click={handleShowImpressum}>
        <img src="/images/impressum.gif" alt="Impressum" class="footer-gif" />
        <div>Impressum</div>
      </button>
    </div>
  {/if}
  {#if showPopupLinks}
    <PopupLinks onClose={handleClosePopupLinks} />
  {/if}
  {#if showAbout}
    <About onClose={handleCloseAbout} />
  {/if}
  {#if showImpressum}
    <Impressum onClose={handleCloseImpressum} />
  {/if}
  {#if showDraggablePopup}
    <DraggablePopup onClose={handleCloseDraggablePopup} />
  {/if}
</main>

<style>
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f0f0f0;
  }

  .footer-links {
    position: fixed;
    bottom: 10px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    gap: 20px;
  }

  .footer-link {
    display: flex;
    flex-direction: column;
    align-items: center;
    cursor: pointer;
  }

  .footer-gif {
    width: 50px;
    height: auto;
  }

  .footer-link div {
    text-align: center;
    margin-top: 5px;
    font-family: "Microsoft Sans Serif", sans-serif;
    font-size: 12px;
    color: white;
  }

  button {
    background: none;
    border: none;
    cursor: pointer;
    padding: 5px;
  }
</style>
