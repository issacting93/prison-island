<script>
  import { onDestroy } from "svelte";
  import { beforeUpdate, afterUpdate } from "svelte";
  export let count = 0;
  export let role;
  import Loader from "./Loader.svelte";

  export let selectedPage;

  export let selectedPageUrl;
  let waiting = 0;

  const notifyLoaded = () => {
    console.log("loaded!");
  };

  const onload = (el) => {
    waiting++;
    el.addEventListener("load", () => {
      waiting--;
      if (waiting === 0) {
        notifyLoaded();
      }
    });
  };
  let elapsed = 0;
  export let duration = 5000;

  let last_time = window.performance.now();
  let frame;

  (function update() {
    frame = requestAnimationFrame(update);

    const time = window.performance.now();
    elapsed += Math.min(time - last_time, duration - elapsed);

    last_time = time;
  })();
  afterUpdate(() => {
    if (duration == elapsed) {
      if (role == "Warden") {
        window.open("/Stage04/W/index.html", "_self");
      } else {
        window.open("/Stage04/P/index.html", "_self");
      }
      count += 1;
      elapsed = 0;
    }
  });
  onDestroy(() => {
    cancelAnimationFrame(frame);
  });

  setTimeout(openUrl, 20000); // Wait 5 secondsx
  function openUrl() {
    if (role == "Warden") {
      window.open("/Stage04/W/index.html", "_self");
    } else {
      window.open("/Stage04/P/index.html", "_self");
    }
  }
</script>

<audio
  style="position:absolute; right:0px;z-index:10;"
  preload="auto"
  autoplay
  loop
  src="Audio/221113_iRiot Stage 4 Priosner_Timestamp.mp3"
/>

<div class="escape-container">
  <Loader />

  {#if role == "Warden"}
    <a href="/Stage04/W/index.html">
      <div class="item-container" />
    </a>
  {:else}
    <a href="/Stage04/P/index.html">
      <div class="item-container" />
    </a>{/if}
</div>

<style>
  .choice-box {
    column-gap: 20px;
    row-gap: 10px;
  }
  .item-container {
    width: 1600px;
    background-size: contain;
    height: 900px;
    max-width: 100vw;
    margin: 10px auto;
    background-image: url("/Images/count-down.gif");
    background-repeat: no-repeat;
    background-position: center;
  }
</style>
