<script>
  import { onMount } from "svelte";
  export let count = 0;
  export let selectedPageUrl;
  export let role;
  export let selectedPage;
  import Loader from "./Loader.svelte";
  let book;
  let bookOpen = false;
  import stages from "../data.json";
  import utility from "../util.json";
  let characterState = 4;
  let character01State = 4;
  let character02State = 4;
  let character03State = 4;
  let character04State = 4;
  function handleClick() {
    count += 1;
    playClick();
  }

  function backClick() {
    count -= 1;
  }
  function openItem(clickedBook) {
    bookOpen = true;
    book = clickedBook;
    playClick();
  }
  function closeItem() {
    bookOpen = false;
    playClick();
  }
  function clickCharacter() {
    characterState += 1;
    playClick();
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

  function clickCharacter01() {
    character01State += 1;

    if (character01State >= stages[count].character01.length) {
      character01State = 4;
    }
    playClick();
  }
  function clickCharacter02() {
    character02State += 1;
    console.log(character02State);
    if (character02State >= stages[count].character02.length) {
      character02State = 4;
    }
    playClick();
  }
  function clickCharacter03(characterState) {
    character03State += 1;
    playClick();
  }
  function clickCharacter04(characterState) {
    character04State += 1;
    playClick();
  }
</script>

<div>
  <button
    class="back-button animated fadeIn"
    on:click={backClick}
    style="background-image:{utility[0].next}"
  />
  <audio src={sound} bind:this={audio} />
  <Loader />
  {#if role == "Warden"}
    <div
      class="item-container animated animatedFadeInUp fadeIn"
      style="background-image:{stages[count].img02};"
    >
      <audio
        style="position:absolute; right:0px;z-index:10;"
        preload="auto"
        autoplay
        loop
        src="Audio/Music/221113_iRiot_Stage 2 Warden Dorm.mp3"
      />
      <button
        on:click={() => clickCharacter01()}
        class="character item"
        style="background-image:{stages[count].character01[character01State]};
          width:{stages[count].character01[0]};
          height:{stages[count].character01[1]};
          left:{stages[count].character01[2]};
          top:{stages[count].character01[3]}; "
      />
      <button
        on:click={() => clickCharacter02(character02State)}
        class="character item"
        style="background-image:{stages[count].character02[character02State]};
        width:{stages[count].character02[0]};
        height:{stages[count].character02[1]};
        left:{stages[count].character02[2]};
        top:{stages[count].character02[3]}; "
      />
      <button
        id="item-01"
        class="item-01 item"
        on:click={openItem(stages[count].img01itemW01[2])}
        style="left: {stages[count].img01itemW01[0]} ; top: {stages[count]
          .img01itemW01[1]} ;  background-image:  {stages[count]
          .img01itemW01[3]};  width: {stages[count]
          .img01itemW01[5]}; height:{stages[count].img01itemW01[6]};"
      />
      <button
        id="item-02"
        class="item-02 item"
        on:click={openItem(stages[count].img01itemW02[2])}
        style="left: {stages[count].img01itemW02[0]} ; top: {stages[count]
          .img01itemW02[1]} ; background-image:  {stages[count]
          .img01itemW02[3]}; width: {stages[count]
          .img01itemW02[5]}; height:{stages[count].img01itemW02[6]}; "
      />
      <button
        id="item-03"
        class="item-03 item"
        on:click={openItem(stages[count].img01itemW03[2])}
        style="left: {stages[count].img01itemW03[0]} ; top: {stages[count]
          .img01itemW03[1]} ;  background-image:  {stages[count]
          .img01itemW03[3]}; width: {stages[count]
          .img01itemW03[5]}; height:{stages[count].img01itemW03[6]}; "
      />
      <button
        id="item-04"
        class="item-04 item"
        on:click={openItem(stages[count].img01itemW04[2])}
        style="left: {stages[count].img01itemW04[0]} ; top: {stages[count]
          .img01itemW04[1]} ; background-image: {stages[count]
          .img01itemW04[3]};width: {stages[count]
          .img01itemW04[5]};  height:{stages[count].img01itemW04[6]}; "
      />
      <button
        id="item-05"
        class="item-05 item"
        on:click={openItem(stages[count].img01itemW05[2])}
        style="left: {stages[count].img01itemW05[0]} ; top: {stages[count]
          .img01itemW05[1]} ; background-image: {stages[count]
          .img01itemW05[3]};width: {stages[count]
          .img01itemW05[5]};  height:{stages[count].img01itemW05[6]}; "
      />
    </div>

    {#if bookOpen == true}
      <div class="modal animated animatedFadeInUp  fadeIn">
        <button
          class="close-btn"
          on:click={() => closeItem()}
          style="background-image:{utility[0].back}"
        />
        <div id="magazine">
          <div class="iframe-container animated animatedFadeInUp fadeIn">
            <iframe src={book} frameborder="0" />
          </div>
        </div>
      </div>
    {:else}{/if}
  {:else}
    {#if bookOpen == true}
      <div class="modal animated animatedFadeInUp fadeInUp">
        <button
          class="close-btn"
          on:click={() => closeItem()}
          style="background-image:{utility[0].back}"
        />
        <div id="magazine">
          <div class="iframe-container animated animatedFadeInUp fadeInUp">
            <iframe src={book} frameborder="0" />
          </div>
        </div>
      </div>
    {:else}{/if}

    <div
      class="item-container   animated animatedFadeInUp fadeInUp"
      style="background-image:{stages[count].img01};"
    >
      <audio
        style="position:absolute; right:0px;z-index:10;"
        preload="auto"
        autoplay
        loop
        src="Audio/Music/221113_iRiot_Stage 2 Prisoner Dorm.mp3"
      />
      <button
        id="item-01"
        class="item-01 item"
        on:click={openItem(stages[count].img01itemP01[2])}
        style="left: {stages[count].img01itemP01[0]} ; top: {stages[count]
          .img01itemP01[1]} ;   background-image:  {stages[count]
          .img01itemP01[3]}; width: {stages[count]
          .img01itemP01[5]}; height:{stages[count].img01itemP01[6]}; "
      />
      <button
        id="item-02"
        class="item-02 item"
        on:click={openItem(stages[count].img01itemP02[2])}
        style="left: {stages[count].img01itemP02[0]} ; top: {stages[count]
          .img01itemP02[1]} ;  background-image:  {stages[count]
          .img01itemP02[3]};  width: {stages[count]
          .img01itemP02[5]};height:{stages[count].img01itemP02[6]};"
      />
      <button
        id="item-03"
        class="item-03 item"
        on:click={openItem(stages[count].img01itemP03[2])}
        style="left: {stages[count].img01itemP03[0]} ; top: {stages[count]
          .img01itemP03[1]}  ;  background-image:  {stages[count]
          .img01itemP03[3]};width: {stages[count]
          .img01itemP03[5]};  height:{stages[count].img01itemP03[6]}; "
      />
      <button
        id="item-04"
        class="item-04 item"
        on:click={openItem(stages[count].img01itemP04[2])}
        style="left: {stages[count].img01itemP04[0]} ; top: {stages[count]
          .img01itemP04[1]}  ;  background-image:  {stages[count]
          .img01itemP04[3]}; width: {stages[count]
          .img01itemP04[5]}; height:{stages[count].img01itemP04[6]};"
      />
      <button
        id="item-05"
        class="item-04 item"
        on:click={openItem(stages[count].img01itemP05[2])}
        style="left: {stages[count].img01itemP05[0]} ; top: {stages[count]
          .img01itemP05[1]}  ;  background-image:  {stages[count]
          .img01itemP05[3]}; width: {stages[count]
          .img01itemP05[5]}; height:{stages[count].img01itemP05[6]};"
      />
      <button
        id="item-06"
        class="item-06 item"
        on:click={openItem(stages[count].img01itemP06[2])}
        style="left: {stages[count].img01itemP06[0]} ; top: {stages[count]
          .img01itemP06[1]} ; background-image: {stages[count]
          .img01itemP06[3]};width: {stages[count]
          .img01itemP06[5]};  height:{stages[count].img01itemP06[6]}; "
      />
    </div>
  {/if}
  <button
    class="next-button"
    on:click={handleClick}
    style="background-image:{utility[0].next}"
  />
</div>

<style>
  button {
    background-size: contain;
    border: 0px solid white;
    background-repeat: no-repeat;
    background-position: center;
    padding: 8px;
    margin: 12px;
    color: black;
  }
  div#magazine {
    width: 100%;
    height: 100%;
    background-color: rgba(1, 1, 1, 0.1);
    position: absolute;
    top: 0px;
  }

  .close-btn {
    position: fixed;
    color: black;
    z-index: 100;
    bottom: 0px;
    height: 60px;
    width: 60px;
    background-color: transparent;
    top: 0%;
    right: 0%;
  }

  button:hover {
    opacity: 0.8;
    filter: sepia(100%) hue-rotate(312deg) saturate(4) contrast(3.5);
  }

  .next-button:hover {
    filter: brightness(1);
  }

  .back-button:hover {
    filter: brightness(1);
  }
  .character {
  }

  .modal {
    position: fixed;
    background: rgba(76, 65, 51, 0.8);
    height: 100vh;
    z-index: 100;
    top: 0px;
    width: 100vw;
    left: 0px;
    right: 0px;
    display: flex;
    justify-content: center;
    animation-duration: 3s !important;
    animation-fill-mode: both;
    -webkit-animation-duration: 3s !important;
    -webkit-animation-fill-mode: both;
  }
  .item-container {
    margin: auto;
    width: 100%;
    padding-top: 56.25%;
    position: relative;
    background-size: contain;
    background-repeat: no-repeat;
    background-position: top;
    background-color: transparent;
  }

  .item {
    position: absolute;
    background-size: contain;
    background-repeat: no-repeat;
    padding: 0px;
    margin: 0px;

    background-color: transparent;
  }

  .item-02 {
    top: 150px;
    left: 200px;
  }

  .item-03 {
    top: 20px;
    left: 250px;
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
