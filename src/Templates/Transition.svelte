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

<audio
  style="position:absolute; right:0px;z-index:10;"
  preload="auto"
  loop
  autoplay
  src="Audio/Music/Waves.mp3"
/>

<div class="transition container" on:click={handleClick}>
  <div class="splashpage" />
  <div class="opening" />
  <audio src={sound} bind:this={audio} />
</div>

<style>
  video {
    position: absolute;
    transform: translate(-50%, -50%);
  }
  .splashpage {
    background-image: url("../Images/00---Splash-Page.gif");
    width: 1600px;
    aspect-ratio: 16/9;
    z-index: 11;
  }

  .container {
    justify-content: center;
    flex-direction: column;
    margin: 10px auto;
    cursor: pointer;
  }
  .opening {
    background-image: url("../Images/Common/opening.png");
    position: fixed;
    width: 100%;
    height: 100vh;
    top: 0px;
    left: 0px;
    filter: blur(10px);
    margin: auto;
    opacity: 0.2;
    background-repeat: no-repeat;
    background-position: center;
    background-size: contain;
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
  .back-button {
    height: 80px;
    width: 80px;
    background-size: cover;
    margin: auto;
    border: 0px black solid;
    margin-top: 20px;
    position: absolute;
    left: 40px;
    border-radius: 100%;
    top: 50%;
    bottom: 50%;
    transform: translate(0px, -50%) rotate(180deg);
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
</style>
