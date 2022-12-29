<script>
  import { createEventDispatcher } from "svelte";
  import { onMount } from "svelte";
  export let count = 0;
  import stages from "../data.json";
  import utility from "../util.json";

  import { fade } from "svelte/transition";
  const dispatch = createEventDispatcher();
  let imgP = stages[count].imgP;
  let imgW = stages[count].imgW;
  let title = stages[count].title;
  import Loader from "./Loader.svelte";
  export let inputSelectedRole = "None";

  onMount(() => {
    inputSelectedRole = undefined;
  });
  function handleClick(role) {
    count += 1;
    inputSelectedRole = role;
    playClick();
  }

  function backClick() {
    count -= 1;
  }
  let audio;
  let sound;

  function playClick() {
    if (audio.paused) {
      sound = "Audio/SFX/Clicking_SFX.mp3";
      audio.play();
    } else {
      audio.currentTime = 0;
    }
  }
</script>

<Loader />
<button
  class="back-button animated fadeIn"
  on:click={backClick}
  style="background-image:{utility[0].next}"
/>
<audio
  style="position:absolute; right:0px;z-index:10;"
  preload="auto"
  autoplay
  src="Audio/Music/Choose Your Character.mp3"
>
  Your browser does not support the audio element.
</audio>
<div
  class="main-container"
  style="background-image:{stages[count].titleImg}"
  transition:fade
>
  <div class="card-container">
    <button on:click={() => handleClick("Warden")}>
      <div class="img warden animated animatedFadeInUp fadeIn" />
    </button>
  </div>

  <div class="card-container">
    <button on:click={() => handleClick("Prisoner")}>
      <div class="img prisoner animated animatedFadeInUp fadeIn" />
    </button>
  </div>
</div>

<style>
  div#preload {
    display: none;
  }
  .img {
    height: 100%;
    background-image: url(border.png);
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center;
    margin: 24px;
  }
  .main-container {
    display: flex;
    justify-content: center;
    background-size: contain;
    position: relative;
    background-position: center;
    width: 100%;
    height: 100%;
    margin: auto;
    max-width: 1600px;
    background-repeat: no-repeat;
    align-items: center;
  }
  .card-container {
    display: flex;
    flex-direction: column;
    min-width: 300px;
    justify-content: center;
    width: auto;
    height: 82.806%;
    width: 35.5625%;
  }

  button {
    background-size: contain;
    border: 0px solid white;
    background-repeat: no-repeat;
    color: white;
    background-size: cover;
    height: 100%;
    padding: 8px;
    margin: 12px;
    transition: 0.4s all;
    background-color: rgba(1, 1, 1, 0);
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

  .warden {
    filter: grayscale(100%);
    transition: 0.4s all;
    background-image: url("../Images/Stage01/Warden-unselected.png");
    background-position: right;
  }
  .warden:hover {
    filter: grayscale(0%);
    background-image: url("../Images/Stage01/Warden-selected.png");
  }
  .prisoner {
    filter: grayscale(100%);
    transition: 0.4s all;
    background-image: url("../Images/Stage01/Prisoner-unselected.png");
    background-position: left;
  }
  .prisoner:hover {
    filter: grayscale(0%);
    background-image: url("../Images/Stage01/Prisoner-selected.png");
  }

  /* Animation */

  @keyframes fadeInUp {
    from {
      transform: translate3d(0, 40px, 0);
    }

    to {
      transform: translate3d(0, 0, 0);
      opacity: 1;
    }
  }

  @-webkit-keyframes fadeInUp {
    from {
      transform: translate3d(0, 40px, 0);
    }

    to {
      transform: translate3d(0, 0, 0);
      opacity: 1;
    }
  }

  @keyframes fadeIn {
    from {
    }

    to {
      opacity: 1;
    }
  }

  @-webkit-keyframes fadeIn {
    from {
    }

    to {
      opacity: 1;
    }
  }

  .animated {
    animation-duration: 1s;
    animation-fill-mode: both;
    -webkit-animation-duration: 1s;
    -webkit-animation-fill-mode: both;
  }

  .animatedFadeInUp {
    opacity: 0;
  }

  .fadeInUp {
    opacity: 0;
    animation-name: fadeInUp;
    -webkit-animation-name: fadeInUp;
  }

  .fadeIn {
    opacity: 0;
    animation-name: fadeIn;
    -webkit-animation-name: fadeIn;
  }
</style>
