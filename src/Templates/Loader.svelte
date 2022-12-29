<script>
  import { onMount } from "svelte";
  const loader = document.querySelector(".loader");
  onMount(async () => {
    setTimeout(() => {
      let Loader = document.getElementById("loader");
      if (Loader === null) {
      } else {
        Loader.style.display = "none";
      }
    }, 2000);
  });
</script>

<div class="loader" id="loader">
  <div class="loading-text">Loading...</div>
</div>

<style>
  @-webkit-keyframes fadeOut {
    0% {
      opacity: 1;
    }
    70% {
      opacity: 1;
      width: 100%;
      height: 100%;
    }
    100% {
      opacity: 0;
    }
  }
  @keyframes fadeOut {
    0% {
      opacity: 1;
    }
    70% {
      opacity: 1;
      width: 100%;
      height: 100%;
    }
    100% {
      opacity: 0;
    }
  }
  .loader {
    background: black;
    width: 100vw;
    height: 100vh;
    position: fixed;
    z-index: 1000;
    animation-delay: 12s;
    -webkit-animation: fadeOut 1.3s;
    animation: fadeOut 1.3s;
    animation-fill-mode: forwards;
    left: 0px;
    right: 0px;
    top: 0px;
  }
</style>
