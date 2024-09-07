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
      <a href="javascript:void(0)" on:click={handleShowAbout}>About</a>
      <a href="javascript:void(0)" on:click={handleShowImpressum}>Impressum</a>
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
  }

  .footer-links {
    position: fixed;
    bottom: 10px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    gap: 20px;
    z-index: 1000;
  }

  .footer-links a {
    color: white;
    text-decoration: none;
    font-family: "Microsoft Sans Serif", sans-serif;
    font-size: 12px;
  }

  .footer-links a:hover {
    text-decoration: underline;
  }
</style>
