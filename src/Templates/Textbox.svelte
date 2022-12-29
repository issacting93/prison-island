<script>
  import stages from "../data.json";
  import utility from "../util.json";
  import Timer from "./Timer.svelte";
  import Loader from "./Loader.svelte";
  import ButtonGroup from "./ButtonGroup.svelte";

  export let selectedPage;
  export let selectedPageUrl;
  export let inputSelectedRole;
  export let role;
  export let count;
  let textNumber = 0;
  let textPBoxSize = stages[count].textboxPimg.length;
  let textWBoxSize = stages[count].textboxWimg.length;
  let imgP = stages[count].imgP;
  let imgW = stages[count].imgW;
  let lastboxW = textWBoxSize - 1;
  let lastboxP = textPBoxSize - 1;
  let optionsW = stages[count].optionsW;
  let optionsP = stages[count].optionsP;
  let characterState = 1;
  let reply = false;
  let notClicked = true;
  let selectOption = true;

  function handleClick(option) {
    reply = true;
    playSound("click");

    timer();
    selectedPage = option;
    notClicked = false;
    characterState = 2;
    if (characterState > 5) {
      characterState = 2;
    }
  }

  function backClick() {
    count -= 1;
  }
  function nextText(selectedTextbox) {
    playSound("click");
    textNumber += 1;
    if (selectedTextbox == textNumber) {
      selectOption = false;
      textNumber = 0;
    }
  }
  function backText(selectedTextbox) {
    playSound("click");
    textNumber -= 1;
    if (selectedTextbox == textNumber) {
      selectOption = false;
      textNumber = 0;
    }
  }
  function delay(time) {
    return new Promise((resolve) => setTimeout(resolve, time));
  }

  async function timer() {
    console.log("start timer");
    await delay(1500);
    console.log("after 1 second");
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

<button
  class="back-button animated fadeIn"
  on:click={backClick}
  style="background-image:{utility[0].next}"
/>
<audio preload="auto " src="Audio/SFX/Clicking_SFX.mp3" bind:this={audio} />
<audio
  style="position:absolute; right:0px;z-index:10;"
  preload="auto"
  autoplay
  loop
  src="Audio/Music/Welcome to Pulau Senang.mp3"
/>
{#if role == "Warden"}
  <Loader />
  <div class="text-box-container  img animated animatedFadeInUp fadeInUp">
    <div class="img-background" style=" background-image:{imgW};">
      <div style="background-image:url(Images/TextW).png;">
        <div
          class="character animated animatedFadeInUp fadeInUp"
          style="background-image:{stages[count].characterW[characterState]}"
        />
      </div>
    </div>

    {#if selectOption}
      <div
        class="text-box animated animatedFadeInUp fadeInUp"
        style="background-image:{utility[0].textbox}"
      >
        {#if lastboxW >= textNumber}
          <!--
 <div class="header">{stages[count].characterW[0]}</div>
        -->
          <div class="text-row ">
            <div
              class="text-img"
              style="background-image:{stages[count].textboxWimg[textNumber]}"
            />
            <!--
             <div class="text  animated animatedFadeInUp fadeInUp">
              {stages[count].textW[textNumber]}
            </div>
          -->

            <div class="button-wrapper">
              {#if textNumber > 0}
                <button
                  class="next-button flip "
                  on:click={() => backText(textWBoxSize)}
                  style="background-image:{utility[0].textboxnext}"
                />{/if}
              <button
                class="next-button"
                on:click={() => nextText(textPBoxSize)}
                style="background-image:{utility[0].textboxnext}"
              />
            </div>
          </div>
        {:else}{/if}
      </div>
    {:else}
      <div class="option-box  " style="background-image:{utility[0].optionbox}">
        <div class="options-container">
          <button
            class="option-button "
            style="background-image:url('Images/Stage01/option 1.png')"
            on:click={() => handleClick("Plantation")}
          />
          <button
            class="option-button "
            style="background-image:url('Images/Stage01/option 2.png')"
            on:click={() => handleClick("Construction")}
          />
          <!--
          <div class="card-container">
            <ul>

 {#each optionsW as option, i}
                <li>
                  <div
                    class="arrow"
                    style="background-image:{utility[0].arrow}"
                  />
                  <ButtonGroup>
                    <button
                      class="option-button"
                      on:click={() => handleClick(option, i)}
                    >
                      {option[0]}
                    </button>
                  </ButtonGroup>
                </li>
              {/each}

            </ul>
          </div>
           -->
        </div>
      </div>
    {/if}
  </div>
{:else}
  <Loader />
  <div class="text-box-container  img animated animatedFadeInUp fadeInUp">
    <div class="img-background" style=" background-image:{imgP};">
      <div style="background-image:url(Images/TextP).png;">
        <div
          class="character animated animatedFadeInUp fadeInUp"
          style="background-image:{stages[count].characterP[characterState]}"
        />
      </div>
    </div>

    <br />
    {#if selectOption}
      <div
        class="text-box animated animatedFadeInUp fadeInUp"
        style="background-image:{utility[0].textbox}"
      >
        {#if lastboxP >= textNumber}
          <!--
                <div class="header">{stages[count].characterP[0]}</div>
       -->

          <div class="text-wrapper">
            <div
              class="text-img"
              style="background-image:{stages[count].textboxPimg[textNumber]}"
            />
            <!-- <div class="text  animated animatedFadeInUp fadeInUp">
              {stages[count].textP[textNumber]}
            </div>
            -->

            <div class="button-wrapper">
              {#if textNumber > 0}
                <button
                  class="next-button flip "
                  on:click={() => backText(textWBoxSize)}
                  style="background-image:{utility[0].textboxnext}"
                />{/if}
              <button
                class="next-button"
                on:click={() => nextText(textPBoxSize)}
                style="background-image:{utility[0].textboxnext}"
              />
            </div>
          </div>
        {:else}{/if}
      </div>
    {:else}
      <div class="option-box  " style="background-image:{utility[0].optionbox}">
        <div class="options-container">
          <button
            class="option-button "
            style="background-image:url('Images/Stage01/option 1.png')"
            on:click={() => handleClick("Plantation")}
          />
          <button
            class="option-button "
            style="background-image:url('Images/Stage01/option 2.png')"
            on:click={() => handleClick("Construction")}
          />
          <!--
 {#each optionsP as option, i}
              <li>
                <button
                  class="option-button"
                  on:click={() => handleClick(option, i)}
                >
                  <div
                    class="arrow"
                    style="background-image:{utility[0].arrow}"
                  />
                  {option[0]}
                </button>
              </li>
            {/each}
            -->
        </div>
      </div>
    {/if}
  </div>
{/if}

<style>
  ul {
    display: none;
  }
  div#preload {
    display: none;
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
  .header {
    font-weight: 900;
    font-size: 28px;
    padding-left: 100px;
    padding-top: 10px;
    color: white;
    font-family: "CrimsonPro";
    font-size: 2rem;
  }
  .button-wrapper {
    position: relative;
    display: flex;
    flex-direction: row;
    margin-right: 20px;
    align-content: center;
    min-width: 140px;
    height: 100%;
    align-items: center;
    justify-content: flex-end;
  }
  .text-img {
    width: 100%;
    height: 59%;
    background-repeat: no-repeat;
    margin-left: 12%;
    background-size: contain;
    margin-right: 2%;
    margin-top: 3%;
  }
  ul {
    list-style-type: none; /* Remove bullets */
    padding: 0; /* Remove padding */
    margin: 0; /* Remove margins */
    display: flex;
    flex-direction: column;
  }
  li {
    display: flex;
    width: 100%;
    align-content: center;
    align-items: center;
  }
  .next {
    margin: 0px 40px;
  }
  .arrow {
    height: 16px;
    width: 45px;
    background-repeat: no-repeat;
    background-size: contain;
  }
  .character {
    height: 85.026%;
    width: 51.375%;
    background-size: contain;
    bottom: 0px;
    position: absolute;
    left: 50px;
    background-repeat: no-repeat;
    display: inline-block;
    animation-delay: 0.8s;
    background-position-y: bottom;
  }

  .text-box {
    display: flex;
    flex-direction: column;
    text-align: left;
    height: 29.193%;
    padding: 24px;
    width: 57.875%;
    color: black;
    background-repeat: no-repeat;
    background-size: contain;
    font-size: 1.7rem;
    margin: 10px;
    animation-delay: 0.9s;
    margin-right: 5.875%;
  }
  .option-box {
    display: flex;
    flex-direction: column;
    text-align: left;
    height: 21.75%;
    width: 52.625%;
    color: black;
    animation-delay: 0.9s;
    background-size: contain;
    bottom: 50px;
    right: 5.875%;
    background-repeat: no-repeat;
    margin-right: 5.875%;
    font-size: 1.7rem;
    justify-content: center;
    margin-bottom: 50px;
  }
  .text-box-reply {
    display: flex;
    flex-direction: column;
    text-align: left;
    height: 150px;
    padding: 24px;
    width: 620px;
    color: black;
    background-size: contain;
    margin: 10px;
    background-image: url(Images/reply_speech.png);
  }

  .text {
    padding-left: 100px;
    max-width: 540px;
    font-family: "CrimsonPro";
    font-size: 1.5rem;
    padding-top: 12px;
  }
  .text-box-container {
    max-height: 100vh;
    display: flex;
    align-items: flex-end;
    justify-content: flex-end;
    max-width: 1600px;
    margin: auto;
    min-width: 1100px;
    aspect-ratio: 16/9;
  }
  .options-container {
    background: transparent;
    border-radius: 0px;
    margin: 4px;
    color: black;
    height: 100%;
    text-align: left;
    padding: 2.664% 1.5%;
    padding-left: 20px;
    display: flex;
    font-size: 19px;
    font-family: "CrimsonPro";
    align-content: center;
    align-items: center;
    flex-direction: column;
    justify-content: center;
  }

  .img {
    height: 100%;

    background-size: contain;
    background-repeat: no-repeat;
    background-position: center;
  }
  .text-wrapper {
    display: flex;
    flex-direction: row;
    height: 100%;
    justify-content: space-between;
    align-content: center;
    align-items: flex-start;
  }
  .img-background {
    background-size: cover;
    position: absolute;
    width: 100%;
    height: 100%;
    z-index: -1;
    display: flex;
  }
  .text-row {
    display: flex;
    justify-content: space-between;
    height: 100%;
    align-items: flex-start;
  }
  .card-container {
    display: flex;
    flex-direction: column;
    width: auto;
    margin-top: -11px;
  }

  button {
    background-size: contain;
    border: 0px solid white;
    background-repeat: no-repeat;
    color: white;
    background-position: center;
    margin: 4px;
    transition: 0.2s all;
    height: 40px;
    width: 40px;
    border-radius: 110px;
  }
  .next-button {
    display: block;
    position: relative;
    left: 0px;
    right: 0px;
    top: 0px;
    margin-bottom: 35%;
    transform: none;

    height: 60px;
    width: 100%;
    max-width: 60px;
    background-color: transparent;
  }

  .flip {
    transform: rotate(180deg);
  }

  .option-button {
    display: flex;
    flex-direction: row;
    background: transparent;
    width: auto;
    border-radius: 0px;
    margin: 4px;
    color: black;
    text-align: left;
    margin: 0px;
    padding: 0px;
    align-content: center;
    width: 100%;
    align-items: center;
    font-size: 1.7rem;
    background-repeat: no-repeat;
  }
  button:hover {
    opacity: 0.3;
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
  @media screen and (max-width: 1292px) {
    .text {
      font-size: 1.25rem;
    }

    .option-button {
      font-size: 1.25rem;
    }

    .header {
      padding-left: 70px;
      padding-top: 0px;
    }
    .text {
      padding-left: 70px;
    }
    .text-box-container {
      max-height: 100vh;
      margin: auto;
      min-width: 0px;
      aspect-ratio: 16/9;
    }
  }
</style>
