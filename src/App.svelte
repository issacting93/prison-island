<script>
  import ChooseCharacterPage from "./Templates/ChooseCharacterPage.svelte";

  import Transition from "./Templates/Transition.svelte";
  import Video from "./Templates/Video.svelte";

  import Video2 from "./Templates/Video2.svelte";
  import RoleIndicator from "./Templates/RoleIndicator.svelte";
  import ItemDetails from "./Templates/ItemDetails.svelte";
  import ItemDetails2 from "./Templates/ItemDetails2.svelte";
  import EscapeChoice from "./Templates/EscapeChoice.svelte";
  import Biography from "./Templates/Biography.svelte";

  import utility from "./util.json";
  import Slate from "./Templates/Slate.svelte";
  import stages from "./data.json";
  import Textbox from "./Templates/Textbox.svelte";
  import { createLoadObserver } from "./Templates/util.js";
  import AudioPlayer, { stopAll } from "./AudioPlayer.svelte";
  import Analytics from "analytics";
  import googleAnalytics from "@analytics/google-analytics";

  const analytics = Analytics({
    app: "Prison-Island",
    plugins: [
      googleAnalytics({
        measurementIds: ["G-7SPT3P2Y9E"],
      }),
    ],
  });

  /* Track a page view */
  analytics.page();

  /* Track a custom event */
  analytics.track("cartCheckout", {
    item: "pink socks",
    price: 20,
  });

  /* Identify a visitor */
  analytics.identify("user-id-xyz", {
    firstName: "bill",
    lastName: "murray",
  });
  let audioTracks = [
    "./Audio/Music/220926_iRiot_Stage 1 Choose Your Character_Ver2.mp3",
    "./Audio/Music/220926_iRiot_Stage 1 Construction_Ver2.mp3",
    "https://sveltejs.github.io/assets/music/satie.mp3",
  ];
  const onload = createLoadObserver(() => {
    console.log("loaded!!!");
  });
  let state = "start";
  let count = 0;
  let role;
  let selectedRole;
  let currentStage = stages[count].type;
  let selectedPage;
  let selectedPageUrl;
  let isDebugging = false;
  let pausedAudio;
  let player;
  export let src;
  export let paused;
  function handleClick() {
    count += 1;
    if (count >= 5) {
      count = 0;
    } else if (count == 1) {
      audio.play();
      alert("sound");
    }
  }

  function backClick() {
    count -= 1;
    if (count <= 0) {
      count = 0;
    }
  }
  function toggleDebugger() {
    isDebugging = !isDebugging;
  }
  let audio;
  let ambient;
  let book = "credits.html";
  let bookOpen = false;
  let muteText = "Mute All";
  // Mute a singular HTML5 element
  function muteMe(elem) {
    elem.muted = !elem.muted;
    if (elem.muted) {
      elem.pause();
      muteText = "Unmute";
    } else {
      elem.play();
      muteText = "Mute All";
    }
  }

  function openItem() {
    bookOpen = true;
  }

  function closeItem() {
    bookOpen = false;
    playClick();
  }
  // Try to mute all video and audio elements on the page
  function mutePage() {
    document.querySelectorAll("video, audio").forEach((elem) => muteMe(elem));
  }
</script>

<main>
  <iframe
    src="Audio/silence.mp3"
    allow="autoplay"
    id="audio"
    style="display: none"
  />
  <audio
    style="position:absolute; right:0px;z-index:10;"
    preload="auto"
    src="Audio/Music/Waves.mp3"
  />
  <img class="none" src="./Images/Loading-screen.gif" alt="" />
  <div class="loading" />
  {#if bookOpen == true}
    <div class="modal animated animatedFadeInUp  fadeIn">
      <button
        class="close-btn"
        on:click={() => closeItem()}
        style="background-image:{utility[0].back}"
      />

      <div class="iframe-container animated animatedFadeInUp fadeIn">
        <iframe src="credits.html" frameborder="0" />
      </div>
    </div>
  {:else}{/if}
  <div class="main-ui">
    {#if stages[count].type == "ChooseCharacterPage"}
      <ChooseCharacterPage bind:inputSelectedRole={selectedRole} bind:count />
    {:else if stages[count].type == "ItemDetails"}
      <ItemDetails
        bind:count
        role={selectedRole}
        bind:selectedPage
        bind:selectedPageUrl
      />
    {:else if stages[count].type == "ItemDetails2"}
      <ItemDetails2
        bind:count
        role={selectedRole}
        bind:selectedPage
        bind:selectedPageUrl
      />
    {:else if stages[count].type == "Transition"}
      <Transition bind:count role={selectedRole} bind:selectedPage />
    {:else if stages[count].type == "Video"}
      <Video bind:count role={selectedRole} bind:selectedPage />
    {:else if stages[count].type == "Video2"}
      <Video2 bind:count role={selectedRole} bind:selectedPage />
    {:else if stages[count].type == "EscapeChoice"}
      <EscapeChoice
        bind:count
        role={selectedRole}
        bind:selectedPage
        bind:selectedPageUrl
      />
    {:else if stages[count].type == "Textbox"}
      <Textbox
        role={selectedRole}
        bind:count
        bind:selectedPage
        bind:inputSelectedRole={selectedRole}
        bind:selectedPageUrl
      />
    {:else if stages[count].type == "Slate"}
      <Slate
        role={selectedRole}
        bind:count
        bind:selectedPage
        bind:selectedPageUrl
      />
    {:else}
      <Biography bind:count />
    {/if}
  </div>

  <div class="persistent-ui">
    <div class="role-container">
      {#if selectedRole == undefined}{:else}
        <RoleIndicator role={selectedRole} />
      {/if}
    </div>

    <button class="debug-button" on:click={() => (isDebugging = !isDebugging)}>
      Debugger
    </button>

    <button on:click={() => mutePage()}> {muteText}</button>
    {#if isDebugging}
      <button on:click={() => backClick()}>back </button>
      <button on:click={() => openItem()}> Credits </button>
      <div class="debug">
        selected Page : {selectedPage}
        <br />
        Count : {count}
        <br />
        Selected Role :{selectedRole}
      </div>
    {/if}
  </div>
  <div id="preload">
    <img src="./Images/Common/01-02-bg.png" alt="" />
    <img src="./Images/Common/inkblot.png" alt="" />
    <img src="./Images/Common/textbox.png" alt="" />
    <img src="./Images/Common/arrow.png" alt="" />
    <img src="./Images/Common/Next.png" alt="" />
    <img src="./Images/Common/optionbox.png" alt="" />
    <img src="./Images/Stage01/Dutten_State_01.png" alt="" />
    <img src="./Images/Stage01/Prisoner-selected.png" alt="" />
    <img src="./Images/Stage01/Prisoner-unselected.png" alt="" />
    <img src="./Images/Stage01/Warden_Text_1.png" alt="" />
    <img src="./Images/Stage01/Warden_Text_2.png" alt="" />
    <img src="./Images/Stage01/Warden_Text_3.png" alt="" />
    <img src="./Images/Stage01/Prisoner_Text_1.png" alt="" />
    <img src="./Images/Stage01/Prisoner_Text_2.png" alt="" />
    <img src="./Images/Stage01/Prisoner_Text_3.png" alt="" />

    <img src="./Stage01/Images/menu.png" alt="" />
    <img src="./Stage01/Images/chart.png" alt="" />
    <img src="./Images/Stage01/option 1.png" alt="" />
    <img src="./Images/Stage01/option 2.png" alt="" />
    <img src="./Images/Stage01/Warden-selected.png" alt="" />
    <img src="./Images/Stage01/Warden-unselected.png" alt="" />
    <img src="./Images/Stage01/Background-Choose.png" alt="" />
    <img src="./Images/Stage01/7-DAYS-BEFORE-THE-RIOT.gif" alt="" />
    <img src="./Images/Stage01/Construction/cop-speech-01.png" alt="" />
    <img src="./Images/Stage01/Construction/cop-speech-02.png" alt="" />
    <img src="./Images/Stage01/Construction/cop1.png" alt="" />
    <img src="./Images/Stage01/Construction/cop2.png" alt="" />
    <img src="./Images/Stage01/Construction/bg.png" alt="" />
    <img src="./Images/Stage01/Construction/worker1.png" alt="" />
    <img src="./Images/Stage01/Construction/worker2.png" alt="" />
    <img src="./Images/Stage01/Plantation/coconut1.png" alt="" />
    <img src="./Images/Stage01/Plantation/coconut2.png" alt="" />
    <img src="./Images/Stage01/Plantation/cop1.png" alt="" />
    <img src="./Images/Stage01/Plantation/cop2.png" alt="" />
    <img src="./Images/Stage01/Construction/paper.gif" alt="" />
    <img src="./Images/Stage01/Plantation/paper.gif" alt="" />
    <img src="./Images/Stage01/Plantation/coconut.gif" alt="" />
    <img src="./Images/Stage01/Plantation/gardener.gif" alt="" />
    <img src="./Images/Stage01/Plantation/goat.gif" alt="" />
    <img src="./Images/Stage01/Plantation/gardener0.png" alt="" />
    <img src="./Images/Stage01/Plantation/gardener1.png" alt="" />
    <img src="./Images/Stage01/Plantation/gardener2.png" alt="" />
    <img src="./Images/Stage01/Plantation/goat1.png" alt="" />
    <img src="./Images/Stage01/Plantation/goat2.png" alt="" />
    <img src="./Images/Stage01/Plantation/Pie-chart.png" alt="" />
    <img src="./Images/Stage01/Plantation/plantation menu.png" alt="" />
    <img src="./Images/Stage01/Plantation/plantation_bg.png" alt="" />
    <img src="./Stage01/Images/newspaper1.png" alt="" />
    <img src="./Stage01/Images/newspaper2.png" alt="" />
    <img src="./Stage01/Images/newspaper3.png" alt="" />
    <img src="./Stage01/Images/newspaper4.png" alt="" />
    <img src="./Stage01/Images/newspaper5.png" alt="" />
    <img src="./Stage01/Images/newspaper6.png" alt="" />
    <img src="./Images/Stage01/bg.png" alt="" />
    <img src="./Stage02/6-days.png" alt="" />
    <img src="./Images/Stage01/01_dutton_select_L.png" alt="" />
    <img src="./Images/Stage01/01_dutton_select_R.png" alt="" />
    <img src="./Images/Stage01/01_prisoner_select.png" alt="" />
    <img src="./Images/Stage01/01_prisoner_select_left.png" alt="" />
    <img src="./Images/Stage01/01_prisoner_select_right.png" alt="" />
    <img src="./Images/Stage02/02_ganster_default.png" alt="" />
    <img src="./Images/Stage02/02_ganster_select_01.png" alt="" />
    <img src="./Images/Stage02/02_ganster_select_02.png" alt="" />
    <img src="./Images/Stage02/02_ganster_select_03.png" alt="" />
    <img src="./Images/Stage02/6-DAYS-BEFORE-THE-RIOT.gif" alt="" />
    <img src="./Stage02/Prisoner_Quarters.png" alt="" />
    <img src="./Stage02/Warden_Quarters.png" alt="" />
    <img src="./Stage02/Background.png" alt="" />
    <img src="./Images/Stage02/watch.gif" alt="" />
    <img src="./Stage02/cinema-board1.png" alt="" />
    <img src="./Stage02/cinema-board2.png" alt="" />
    <img src="./Stage02/cinema-board3.png" alt="" />
    <img src="./Stage02/Gangster.png" alt="" />
    <img src="./Stage02/Leader.png" alt="" />
    <img src="./Stage02/new-musician-bg.png" alt="" />
    <img src="./Stage02/all_musicians.png" alt="" />
    <img src="./Stage02/Sign-ups.png" alt="" />
    <img src="./Stage02/Recorder-00.png" alt="" />
    <img src="./Stage02/Background.png" alt="" />
    <img src="./Stage02/POP-UP.png" alt="" />
    <img src="./Images/Stage02/chooseP.jpg" alt="" />
    <img src="./Images/Stage02/chooseW.jpg" alt="" />
    <img src="./Stage02/Images/page-last.png" alt="" />
    <img src="./Stage02/Images/page00.png" alt="" />
    <img src="./Stage02/Images/page01-L.png" alt="" />
    <img src="./Stage02/Images/page01-R.png" alt="" />
    <img src="./Stage02/Images/page02-L.png" alt="" />
    <img src="./Stage02/Images/page02-R.png" alt="" />
    <img src="./Stage02/Images/page03-L.png" alt="" />
    <img src="./Stage02/Images/page03-R.png" alt="" />
    <img src="./Stage02/all_musicians.png" alt="" />
   <!-- 
  <video src="./Stage04/Endings/iRiot_Postscript+EndTag_SiteFinal.mp4" />
  
    <img src="./Images/Stage02/Musicians.png" alt="" />
    <img src="./Images/Stage02/background-01.png" alt="" />
    <img src="./Images/Stage02/background-02.png" alt="" />
    <img src="./Images/Stage01/Construction/Map Pop up/map.png" alt="" />
    <img src="./Images/count-down.gif" alt="" />
   -->
  </div>

  <div class="mobile">Please use a desktop for the full experience</div>
</main>

<style>
  .none {
    display: none;
  }
  .loading {
    background-image: url("/Images/Loading-screen.gif");
    position: fixed;
    z-index: 1111;
    height: 100vh;
    width: 100%;
    top: 0px;
    background-size: cover;
    background-repeat: no-repeat;
    animation: loading 13;
    -webkit-animation: loading 13s;
    -moz-animation: loading 13s;
    -o-animation: loading 13s;
    -ms-animation: loading 13s;
    background-position: center;
    animation-fill-mode: forwards;
  }
  button {
    background-color: #1a1a1a;
    cursor: pointer;
    color: white;
  }

  .debug-button {
    width: auto;
    top: 0px;
    position: absolute;
    margin: 8px;
    font-size: 12px;
  }
  .active {
    background-color: pink;
  }

  .modal {
    position: fixed;
    background: rgba(0, 0, 0, 0.5);
    height: 100vh;
    z-index: 100;
    top: 0px;
    width: 100vw;
    left: 0px;
    right: 0px;
    display: flex;
    justify-content: center;
  }
  .debug {
    color: green;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    text-align: right;
    font-size: 12px;
    margin: 8px;
    background-color: #1a1a1a;
    cursor: pointer;
    color: white;
  }

  iframe {
    width: 100%;
    height: 100%;
    position: absolute;
    margin: auto;
    transform: translateX(-50%);
  }

  .iframe-container {
    position: relative;
    height: 100%;
    width: 100%;
  }

  @font-face {
    font-family: "Gelasio";
    font-style: normal;
    font-weight: 400;
    src: local("Gelasio Regular"), local("Gelasio-Regular"),
      url(https://fonts.gstatic.com/s/gelasio/v1/cIf9MaFfvUQxTTqS9C6hYQ.woff2)
        format("woff2");
    unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA,
      U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212,
      U+2215, U+FEFF, U+FFFD;
  }

  .persistent-ui {
    position: absolute;
    z-index: 1000;
    color: green;
    max-width: 1600px;
    margin: auto;
    display: flex;
    width: 100%;
    justify-content: space-between;
    display: flex;
    flex-direction: row;
    transform: translate(-50%, 0px);
    align-items: center;
    left: 50%;
    display: none;
  }
  .main-ui {
    align-content: center;
    height: 100%;
    max-height: 800px;
    overflow: hidden;
    display: flex;
    justify-content: center;
    flex-direction: column;
    max-width: 1600px;
    width: 100%;
    aspect-ratio: 16/9;
  }
  main {
    font-family: sans-serif;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  html {
    background-size: cover;

    height: 100%;
  }
  body {
    min-height: 100%;

    height: 100%;
    background-size: cover;
  }

  .close-btn {
    position: fixed;
    color: black;
    z-index: 100;
    bottom: 0px;
    height: 60px;
    width: 60px;
    background-color: transparent;
    top: 10%;
    right: 10%;
  }

  .role-container {
    left: 0px;
  }
  .mobile {
    position: fixed;
    background-color: #1a1a1a;
    width: 100%;
    height: 100%;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 111;
    top: 0px;
  }

  @keyframes loading {
    98% {
      opacity: 1;
    }
    99% {
      opacity: 0;
      display: block;
      height: 100%;
      width: 100%;
    }
    100% {
      display: none;
      height: 0px;
      opacity: 0;
      width: 0px;
    }
  }
  @media screen and (min-width: 1100px) {
    .mobile {
      display: none;
    }
    #app {
      padding: 0px;
    }
  }
</style>
