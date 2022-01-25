<script>
  import * as sdk from "stem-player-sdk";
  let message = "STEM PLAYER DISCONNECTED";

  async function connect() {
    console.log("TRYING");
    console.log(await sdk.connect());
    message = "STEM PLAYER CONNECTED";
  }

  async function disconnect() {
    await sdk.disconnect();
    message = "STEM PLAYER DISCONNECTED";
  }

  async function tryUpload() {
    const track = {
      title: "Fertilizer",
      vocals:
        "https://storage.googleapis.com/stemshare-songs/fertilizer-7c19aa/1-Fertilizer_vocals.mp3",
      bass: "https://storage.googleapis.com/stemshare-songs/fertilizer-7c19aa/2-Fertilizer_bass.mp3",
      drums:
        "https://storage.googleapis.com/stemshare-songs/fertilizer-7c19aa/3-Fertilizer_drums.mp3",
      other:
        "https://storage.googleapis.com/stemshare-songs/fertilizer-7c19aa/4-Fertilizer_other.mp3",
    };
    //optional fields: two colors, bpm, artist name, title

    try {
      const t = await sdk.generateTrack(track);
      await sdk.upload(t, (uploadInfo) => {
        console.log("UPLOAD IS " + uploadInfo.total + "% DONE");
        message = "UPLOAD IS " + Math.round(uploadInfo.total * 100) + "% DONE";
      });
    } catch (error) {
      console.log(error);
      message = "ERROR UPLOADING";
    }
  }
</script>

<h1>Stem Uploading Demo v1</h1>
<button on:click={connect}>Click</button>
<button on:click={disconnect}>Disconnect</button>
<button on:click={tryUpload}>Upload</button>
<div>{message}</div>
