<script>
	import { onMount } from "svelte";
	export let count = 0;
	export let selectedPage;
	import stages from ".././data.json";
	function handleClick() {
	  count += 1;
	}

	onMount(async () => {
	  switch (selectedPage) {
	    case "option01":
	      alert(stages[count].option01[2]);
	      break;
	    case "option02":
	      alert(stages[count].option02[2]);
	      break;
	    case "option03":
	      alert(stages[count].option03[2]);
	      break;
	    case "option03":
	      alert(stages[count].option03[2]);
	      break;
	    default:
	  }
	});
</script>

<div class="transition container">
{selectedPage}
	<div class="transition-text"> {stages[count].description} </div>
	<iframe width="100%" height="515px" src={stages[count].video} title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<button on:click={handleClick}>
 Next
</button>

</div>

<style>
	.container {
	  display: flex;
	  justify-content: center;
	  flex-direction: column;
	  margin: 10px auto;
	  background: #f7f7f7;
	}
	iframe {
	  margin: auto;
	}
</style>