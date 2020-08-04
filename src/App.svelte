<script>
  import { onMount } from "svelte";

  let videoEl;
  let errorMessage;

  onMount(async () => {
    try {
      const stream = await navigator.mediaDevices.getUserMedia({ video: true });

      videoEl.srcObject = stream;
      videoEl.play();
    } catch (e) {
      console.error(e, "camera access denied");
      errorMessage = "Camera Access Denied";
    }
  });
</script>

<style>
  main {
    width: 100%;
    height: 100vh;
    padding: 0;
    box-sizing: border-box;
    position: absolute;
  }

  video {
    display: block;
    margin: 20px auto;
  }

  h1,
  h2 {
    text-align: center;
  }

  h1 {
    font-size: 40px;
  }

  h2 {
    font-size: 20px;
  }
</style>

<main>
  <h1>Machine Learning</h1>
  <video bind:this={videoEl} width="600" height="480" />

  {#if errorMessage}
    <h2 style="color: red;">{errorMessage}</h2>
  {/if}
</main>
