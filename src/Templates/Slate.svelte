<script>
  import stages from "../data.json";
  import Timer from "./Timer.svelte";
  import utility from "../util.json";
  import Loader from "./Loader.svelte";
  import { dataset_dev } from "svelte/internal";
  import { onMount } from "svelte";
  export let selectedPage;
  export let selectedPageUrl;
  export let role;
  export let count;

  function handleClick() {
    timer();
  }

  function backClick() {
    count -= 1;
  }
  onMount(() => {});
  function delay(time) {
    return new Promise((resolve) => setTimeout(resolve, time));
  }

  async function timer() {
    console.log("start timer");
    playClick();
    await delay(500);
    count += 1;
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

<button
  class="back-button animated fadeIn"
  on:click={backClick}
  style="background-image:{utility[0].next}"
/>
<button
  class="next-button"
  on:click={handleClick}
  style="background-image:{utility[0].next}"
/>
<div class="slate-containter ">
  <audio
    style="position:absolute; right:0px;z-index:10;"
    preload="auto"
    autoplay
    loop
    src="Audio/SFX/Timestamp_SFX.mp3"
  />
  <div
    class=" bg animated fadeIn"
    style=" background-image:url(Images/Common/01-02-bg.png);"
  />
  <div
    class=" ink-background  animated fadeIn"
    style=" background-image:url(Images/Common/inkblot.png);"
  />
  <div
    class="title-img animated fadeIn"
    style=" background-image:{stages[count].titleImg};"
  />

  <audio src={sound} bind:this={audio} />
  <div class="hidden" />
  <!--
  <div class="slate-header">
    {stages[count].title}
  </div>
  <div class="slate-description">
    {stages[count].description}
  </div>-->
</div>

<style>
  .slate-containter {
    display: flex;
    align-content: center;
    justify-content: center;
    flex-direction: column;
    color: white;
    background: black;
    width: 100%;
    height: 100%;
    background-size: cover;
    background-position: center;
    position: relative;
    align-items: center;
  }
  .next-button {
    background-image: url(Images/Next.png);
    margin-left: 80px;
    margin-top: 40px;
    z-index: 111;
  }
  .bg {
    display: flex;
    align-content: center;
    justify-content: center;
    flex-direction: column;
    width: 100%;
    overflow: hidden;
    height: 100%;
    background-size: cover;
    background-position: center;
    position: absolute;
    background-color: rgb(46, 46, 46);
    z-index: 1;
  }
  .ink-background {
    display: flex;
    align-content: center;
    justify-content: center;
    flex-direction: column;
    width: 100%;
    overflow: hidden;
    height: 100%;
    background-position: center;
    position: absolute;
    z-index: 11;
    background-size: cover;
    animation-delay: 500ms;

    background-repeat: no-repeat;
  }
  .title-img {
    display: flex;
    justify-content: center;
    flex-direction: column;
    width: 100%;
    overflow: hidden;
    background-size: cover;
    height: 100%;
    background-position: center;
    position: absolute;
    max-width: 100%;
    z-index: 15;
    animation-delay: 1500ms;
    background-repeat: no-repeat;
    margin: auto;
  }
  .slate-header {
    font-size: 48px;
    font-weight: 400;
    line-height: 120%;
    margin: 16px;
  }

  .slate-description {
    font-size: 16px;
    font-weight: 300;
    margin: 8px;
  }

  .hidden {
    display: none;
  }
</style>
