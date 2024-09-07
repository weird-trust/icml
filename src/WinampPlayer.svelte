<script>
  import { onMount, onDestroy } from "svelte";
  import Webamp from "webamp";
  import PopupLinks from "./PopupLinks.svelte";

  let webamp;
  let showPopup = false;
  let jumpInterval;

  export let startPlaying = false;

  function handleGifClick() {
    showPopup = true;
  }

  function handleClosePopup() {
    showPopup = false;
  }

  function startJumping() {
    const gif = document.querySelector(".bottom-right-gif");
    gif.classList.add("jump");
    setTimeout(() => {
      gif.classList.remove("jump");
    }, 1000); // Animation dauert 1 Sekunde
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
      Math.random() * 500 + 300
    ); // Springe alle 3-8 Sekunden
  });

  onDestroy(() => {
    clearInterval(jumpInterval); // Stoppe das Intervall, wenn die Komponente zerstört wird
  });

  $: if (startPlaying && webamp) {
    webamp.play();
  }
</script>

<div id="winamp-container"></div>
<img
  src="/images/clippy.gif"
  alt="GIF"
  class="bottom-right-gif jump"
  on:click={handleGifClick}
/>

{#if showPopup}
  <PopupLinks onClose={handleClosePopup} />
{/if}

<style>
  #winamp-container {
    width: 100%;
    height: 100%;
  }

  .bottom-right-gif {
    position: fixed;
    bottom: 10px;
    right: 10px;
    width: 100px; /* Passe die Größe des GIFs an */
    height: auto;
    z-index: 1001; /* Stelle sicher, dass das GIF über anderen Elementen liegt */
    cursor: pointer;
    transition: transform 0.5s cubic-bezier(0.5, 0.05, 1, 0.5); /* Übergangseffekt für das Springen */
  }

  .bottom-right-gif.jump {
    transform: translateY(-10px);
  }
</style>
