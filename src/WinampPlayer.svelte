<script>
  import { onMount } from "svelte";
  import Webamp from "webamp";

  let webamp;

  onMount(() => {
    webamp = new Webamp({
      initialTracks: [
        {
          metaData: {
            title: "Internet Changed my Life",
            artist: "A P F L"
          },
          url: "TRACK_URL"
        }
      ],
      initialSkin: {
        url: "Internet_Exlorer_Amp_2.wsz"
      }
    });

    webamp.renderWhenReady(document.getElementById("winamp-container"));

    // SoundCloud API Integration
    const CLIENT_ID = "weird-trust";
    const TRACK_URL = "https://soundcloud.com/weird-trust/test";
    const CORS_PROXY = "https://api.allorigins.win/get?url=";
    const SC_API_URL = `${CORS_PROXY}https://api.soundcloud.com/resolve?url=${TRACK_URL}&client_id=${CLIENT_ID}`;

    fetch(SC_API_URL)
      .then((response) => response.json())
      .then((data) => {
        const track = {
          metaData: {
            title: data.contents.title,
            artist: data.contents.user.username
          },
          url: `${data.contents.stream_url}?client_id=${CLIENT_ID}`
        };
        webamp.appendTracks([track]);
      })
      .catch((error) =>
        console.error("Error fetching SoundCloud track:", error)
      );
  });
</script>

<div id="winamp-container"></div>

<style>
  #winamp-container {
    width: 100%;
    height: 100%;
  }
</style>
