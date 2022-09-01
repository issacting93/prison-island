<script>
	export let count = 0;

	import stages from ".././data.json";
	function handleClick() {
	  count += 1;
	}
</script>

<style>
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

<div id="magazine">
<div class="iframe-container">
<iframe src={stages[count].book} frameborder="0" ></iframe>
</div>

<button on:click={handleClick}>
  Next {count} {count === 1 ? 'time' : 'times'}
</button>

</div>