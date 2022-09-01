<script>
				export let count = 0;
				let book;
				let bookOpen = false;
				import stages from ".././data.json";
				export let role;
				function handleClick() {
				  count += 1;
				}
				function openItem(clickedBook) {
				  bookOpen = true;
				  book = clickedBook;
				}
				function closeItem() {
				  bookOpen = false;
				}
</script>

<div>


<div class='item-container'>
{role}
<button id="item-01" class="item-01 item" on:click={openItem(stages[count].item01[2])}  style="left: {stages[count].item01[0]} ; top: {stages[count].item01[1]} ;  "> </button>
<button id="item-02" class="item-02 item" on:click={openItem(stages[count].item02[2])}  style="left: {stages[count].item02[0]} ; top: {stages[count].item02[1]} ;  "> </button>
<button id="item-03" class="item-03 item" on:click={openItem(stages[count].item03[2])}  style="left: {stages[count].item03[0]} ; top: {stages[count].item03[1]} ;  "> </button>
</div>


{#if bookOpen == true}
<div  class="modal">
<button on:click={() => closeItem()}> Close Book</button>
<div id="magazine">
<div class="iframe-container">
<iframe src={book} frameborder="0" ></iframe>
</div>
</div>
</div>
{:else}
{/if}
<button on:click={handleClick}>
 Next
</button></div>
<style>
  .modal {
    position: absolute;
    background: rgba(0, 0, 0, 0.3);
    height: 100vh;
    z-index: 100;
    top: 0px;
    width: 100vw;
  }
  .item-container {
    background: grey;
    width: 100%;
    height: 90vh;
    position: relative;
  }

  .item {
    width: 200px;
    height: 200px;
    background: blue;
    position: absolute;
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
    height: 600px;
  }
</style>