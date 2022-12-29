<script>
  import { onMount } from "svelte";
  export let count = 0;
  export let selectedPage;
  export let role;
  let textNo = 0;
  let textBoxSize = stages[count].text.length;
  import stages from "../data.json";
  import utility from "../util.json";
  let text = stages[count].text;

  function backClick() {
    count -= 1;
  }
  function handleClick() {
    timer();
  }
  onMount(() => {});
  function delay(time) {
    return new Promise((resolve) => setTimeout(resolve, time));
  }

  async function timer() {
    playSound("click");
    console.log("start timer");
    await delay(500);
    count += 1;
  }
  let audio;
  let sound;
  function playSound(soundtype) {
    if (audio.paused) {
      audio.play();
      switch (soundtype) {
        case "click":
          audio.play();
          sound = "Audio/SFX/Clicking_SFX.mp3";

          // code block
          break;
        case "human":
          sound = "Audio/SFX/Hover_Human.mp3";

          // code block
          break;
        default:
        // code block
      }
    } else {
      audio.currentTime = 0;
    }
  }
</script>

<div class="transition container">
  <audio preload="auto " src="Audio/SFX/Clicking_SFX.mp3" bind:this={audio} />

  <video width="100%" height="100%" controls autoplay>
    <source src={stages[count].video} type="video/mp4" />
    <source src="movie.ogg" type="video/ogg" />
    Your browser does not support the video tag.
  </video>
  <button
    class="back-button animated fadeIn"
    on:click={backClick}
    style="background-image:{utility[0].next}"
  />
  <button
    class="next-button animated fadeIn"
    on:click={handleClick}
    style="background-image:{utility[0].next}"
  />
</div>

<style>
  video {
    position: absolute;
    transform: translate(-50%, -50%);
  }
  .container {
    justify-content: center;
    flex-direction: column;
    margin: 10px auto;
    max-width: 1200px;
  }
  iframe {
    margin: auto;
    max-width: 100%;
  }
  .scrolling-text {
    overflow-y: scroll;
    max-height: 115px;
  }

  .transition-text {
    color: white;
    padding: 10px 10px;
    bottom: 0px;
    left: 0%;
    width: 50%;
    text-align: left;
    position: relative;
  }
  .text {
    padding: 4px 2px;
  }

  .solid-fade {
    position: absolute;
    top: 70%;
    bottom: 0;
    width: 90%;
    background-image: linear-gradient(to bottom, transparent, #1a1a1a);
  }

  /*
   *  STYLE 1
   */

  #style-1::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 3px rgba(255, 255, 255, 1);
    border-radius: 10px;
    background-color: #f5f5f541;
  }

  #style-1::-webkit-scrollbar {
    width: 0px;
    background-color: #f5f5f5;
  }

  #style-1::-webkit-scrollbar-thumb {
    border-radius: 10px;
    -webkit-box-shadow: inset 0 0 3px rgba(255, 255, 255, 1);
    background-color: #555;
  }

  /* Animation */

  @keyframes fadeIn {
    from {
      transform: translate3d(0, 40px, 0);
      opacity: 0;
    }

    to {
      transform: translate3d(0, 0, 0);
      opacity: 1;
    }
  }

  @-webkit-keyframes fadeIn {
    from {
      transform: translate3d(0, 40px, 0);
      opacity: 0;
    }

    to {
      transform: translate3d(0, 0, 0);
      opacity: 1;
    }
  }

  @keyframes fadeIn {
    from {
    }
    20% {
      opacity: 0;
    }

    to {
      opacity: 1;
    }
  }

  @-webkit-keyframes fadeIn {
    from {
    }
    20% {
      opacity: 0;
    }

    to {
      opacity: 1;
    }
  }
  .animated {
    animation-duration: 3s;
    animation-fill-mode: both;
    -webkit-animation-duration: 3s;
    -webkit-animation-fill-mode: both;
  }

  .animatedFadeInUp {
    opacity: 0;
  }

  .fadeIn {
    opacity: 0;
    animation-name: fadeIn;
    -webkit-animation-name: fadeIn;
    animation-timing-function: cubic-bezier(0.165, 0.84, 0.44, 1);
  }
</style>
