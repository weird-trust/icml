<script>
  import { onMount, onDestroy } from "svelte";
  import Webamp from "webamp";
  import SpeechBubble from "./SpeechBubble.svelte";
  import About from "./About.svelte";
  import Platforms from "./Platforms.svelte";
  import ArtistInfo from "./ArtistInfo.svelte";
  import ClippyInfo from "./ClippyInfo.svelte";
  import Impressum from "./Impressum.svelte";
  import Screensaver from "./Screensaver.svelte";
  import PartyMode from "./PartyMode.svelte";

  let webamp;
  let showPopup = false;
  let showAbout = false;
  let showPlatforms = false;
  let showArtistInfo = false;
  let showClippyInfo = false;
  let showImpressum = false;
  let showScreensaver = false;
  let showPartyMode = false;
  let jumpInterval;
  let inactivityTimeout;
  let mouseX = 0;
  let mouseY = 0;

  export let startPlaying = false;

  function handleGifClick() {
    showPopup = true;
  }

  function handlePartyGifClick() {
    showPartyMode = true;
  }

  function handleClosePopup() {
    showPopup = false;
  }

  function handleShowAbout() {
    showAbout = true;
    showPopup = false;
  }

  function handleCloseAbout() {
    showAbout = false;
  }

  function handleShowPlatforms() {
    showPlatforms = true;
    showPopup = false;
  }

  function handleClosePlatforms() {
    showPlatforms = false;
  }

  function handleShowArtistInfo() {
    showArtistInfo = true;
    showPopup = false;
  }

  function handleCloseArtistInfo() {
    showArtistInfo = false;
  }

  function handleShowClippyInfo() {
    showClippyInfo = true;
    showPopup = false;
  }

  function handleCloseClippyInfo() {
    showClippyInfo = false;
  }

  function handleShowImpressum() {
    showImpressum = true;
    showPopup = false;
  }

  function handleCloseImpressum() {
    showImpressum = false;
  }

  function handleShowScreensaver() {
    showScreensaver = true;
  }

  function handleCloseScreensaver() {
    showScreensaver = false;
    resetInactivityTimeout();
  }

  function startJumping() {
    const gif = document.querySelector(".bottom-right-gif");
    gif.classList.add("jump");
    setTimeout(() => {
      gif.classList.remove("jump");
    }, 1000); // Animation dauert 1 Sekunde
  }

  function resetInactivityTimeout() {
    clearTimeout(inactivityTimeout);
    inactivityTimeout = setTimeout(handleShowScreensaver, 10000); // 10 Sekunden Inaktivität
  }

  function handleMouseMove(event) {
    mouseX = event.clientX;
    mouseY = event.clientY;
  }

  onMount(() => {
    webamp = new Webamp({
      initialTracks: [
        {
          metaData: {
            title: "ARP505-Jonas-Gottlieb-Afterhour-Mix",
            artist: "A P F L"
          },
          url: "/audio/ARP505-Jonas-Gottlieb-Afterhour-Mix.mp3"
        },
        {
          metaData: {
            title: "ARP505",
            artist: "A P F L"
          },
          url: "/audio/ARP505.mp3"
        },
        {
          metaData: {
            title: "Dad-Groove",
            artist: "A P F L"
          },
          url: "/audio/Dad-Groove.mp3"
        },
        {
          metaData: {
            title: "Internet_Life",
            artist: "A P F L"
          },
          url: "/audio/Internet_Life.mp3"
        },
        {
          metaData: {
            title: "Neuro-Anwohner-Easly-Mix",
            artist: "A P F L"
          },
          url: "/audio/Neuro-Anwohner-Easly-Mix.mp3"
        },
        {
          metaData: {
            title: "Neuro",
            artist: "A P F L"
          },
          url: "/audio/Neuro.mp3"
        },
        {
          metaData: {
            title: "T6-Christian-Kluge-Remix",
            artist: "A P F L"
          },
          url: "/audio/T6-Christian-Kluge-Remix.mp3"
        },
        {
          metaData: {
            title: "T6",
            artist: "A P F L"
          },
          url: "/audio/T6.mp3"
        },
        {
          metaData: {
            title: "Vactrol-Funk-SV-Breakpoint-Mix.mp3",
            artist: "A P F L"
          },
          url: "/audio/Vactrol-Funk-SV-Breakpoint-Mix.mp3"
        },
        {
          metaData: {
            title: "Vactrol",
            artist: "A P F L"
          },
          url: "/audio/Vactrol.mp3"
        }
      ],
      initialSkin: {
        url: "/Internet_Exlorer_Amp_2.wsz"
      }
    });

    webamp
      .renderWhenReady(document.getElementById("winamp-container"))
      .then(() => {
        if (startPlaying) {
          webamp.play();
        }
      });

    // Starte das Springen in zufälligen Intervallen
    jumpInterval = setInterval(
      () => {
        startJumping();
      },
      Math.random() * 5000 + 3000
    ); // Springe alle 3-8 Sekunden

    // Setze den Inaktivitäts-Timeout
    resetInactivityTimeout();

    // Event-Listener für Benutzeraktivität
    window.addEventListener("mousemove", resetInactivityTimeout);
    window.addEventListener("keydown", resetInactivityTimeout);
    window.addEventListener("mousemove", handleMouseMove);
  });

  onDestroy(() => {
    clearInterval(jumpInterval); // Stoppe das Intervall, wenn die Komponente zerstört wird
    clearTimeout(inactivityTimeout); // Stoppe den Inaktivitäts-Timeout
    window.removeEventListener("mousemove", resetInactivityTimeout);
    window.removeEventListener("keydown", resetInactivityTimeout);
    window.removeEventListener("mousemove", handleMouseMove);
  });

  $: if (startPlaying && webamp) {
    webamp.play();
  }
</script>

<div id="winamp-container" style="width: 100vw; height: 100vh;"></div>
<div class="text-overlay" style="left: {mouseX}px; top: {mouseY}px;"></div>
<img
  src="/images/clippy.gif"
  alt="GIF"
  class="bottom-right-gif jump"
  on:click={handleGifClick}
/>
<img
  src="/images/party.gif"
  alt="Party GIF"
  class="bottom-left-gif"
  on:click={handlePartyGifClick}
/>

{#if showPopup}
  <SpeechBubble
    onClose={handleClosePopup}
    onShowAbout={handleShowAbout}
    onShowPopupLinks={handleShowPlatforms}
    onShowArtistInfo={handleShowArtistInfo}
    onShowClippyInfo={handleShowClippyInfo}
  ></SpeechBubble>
{/if}

{#if showAbout}
  <About onClose={handleCloseAbout} />
{/if}

{#if showPlatforms}
  <Platforms onClose={handleClosePlatforms} />
{/if}

{#if showArtistInfo}
  <ArtistInfo onClose={handleCloseArtistInfo} />
{/if}

{#if showClippyInfo}
  <ClippyInfo onClose={handleCloseClippyInfo} />
{/if}

{#if showImpressum}
  <Impressum onClose={handleCloseImpressum} />
{/if}

{#if showScreensaver}
  <Screensaver onClose={handleCloseScreensaver} />
{/if}

{#if showPartyMode}
  <PartyMode />
{/if}

<style>
  #winamp-container {
    width: 100vw;
    height: 100vh;
  }

  .text-overlay {
    position: fixed;
    font-family: "Comic Sans MS", cursive, sans-serif;
    font-size: 32px;
    color: #2f00ff;
    text-shadow: 2px 2px #000000;
    z-index: 1002;
    transform: translate(-50%, -50%);
    pointer-events: none;
  }

  .bottom-right-gif {
    position: fixed;
    bottom: 10px;
    right: 10px;
    width: 100px;
    height: auto;
    z-index: 1001;
    cursor: pointer;
    transition: transform 0.5s ease-in-out;
  }

  .bottom-left-gif {
    position: fixed;
    bottom: 10px;
    left: 10px;
    width: 100px;
    height: auto;
    z-index: 1001;
    cursor: pointer;
  }

  .bottom-right-gif.jump {
    transform: translateY(-10px);
  }
</style>
