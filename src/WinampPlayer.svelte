<script>
  import { onMount } from "svelte";
  import Webamp from "webamp";

  let webamp;

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

    webamp.renderWhenReady(document.getElementById("winamp-container"));
  });
</script>

<div id="winamp-container"></div>

<style>
  #winamp-container {
    width: 100%;
    height: 100%;
  }
</style>
