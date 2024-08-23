<script>
  import { onMount } from "svelte";
  import Webamp from "webamp";

  let webamp;

  onMount(() => {
    webamp = new Webamp({
      initialTracks: [
        {
          metaData: {
            title: "Sample Track",
            artist: "Sample Artist"
          },
          url: "URL_ZU_DEINER_AUDIODATEI"
        }
      ],
      initialSkin: {
        url: "URL_ZU_DEINEM_WINAMP_SKIN"
      }
    });

    webamp.renderWhenReady(document.getElementById("winamp-container"));

    // SoundCloud API Integration
    const CLIENT_ID = "DEIN_SOUNDCLOUD_CLIENT_ID";
    const TRACK_URL = "URL_ZU_DEINEM_SOUNDCLOUD_TRACK";
    const SC_API_URL = `https://api.soundcloud.com/resolve?url=${TRACK_URL}&client_id=${CLIENT_ID}`;

    fetch(SC_API_URL)
      .then((response) => response.json())
      .then((data) => {
        const track = {
          metaData: {
            title: data.title,
            artist: data.user.username
          },
          url: `${data.stream_url}?client_id=${CLIENT_ID}`
        };
        webamp.appendTracks([track]);
      })
      .catch((error) =>
        console.error("Error fetching SoundCloud track:", error)
      );

    // Bandcamp API Integration (Beispiel, da Bandcamp API spezifischer ist)
    const BANDCAMP_TRACK_URL = "URL_ZU_DEINEM_BANDCAMP_TRACK";
    const BANDCAMP_API_URL = `https://bandcamp.com/api/...`;

    fetch(BANDCAMP_API_URL)
      .then((response) => response.json())
      .then((data) => {
        const track = {
          metaData: {
            title: data.title,
            artist: data.artist
          },
          url: data.stream_url
        };
        webamp.appendTracks([track]);
      })
      .catch((error) => console.error("Error fetching Bandcamp track:", error));
  });
</script>

<div id="winamp-container"></div>

<style>
  #winamp-container {
    width: 100%;
    height: 100%;
  }
</style>
