<script>
			export let count = 0;
			export let selectedPage;
			import stages from ".././data.json";
			function handleClick(option) {
			  count += 1;
			  selectedPage = option;
			}
</script>

<div class="escape-container">

<div class="item-container"></div>
	<div class="choice-box">
		 
<button on:click={() => handleClick("option01")}>
{ stages[count].choices[0]}
</button>
<button on:click={() => handleClick("option02")}>
  { stages[count].choices[1]}
</button>
<button  on:click={() => handleClick("option03")}>
  { stages[count].choices[2]}
</button>
<button  on:click={() => handleClick("option04")}>
  { stages[count].choices[3]}
</button>
 	</div>
</div>

<style>
  .choice-box {
    display: grid;
    grid-template-columns: auto auto;
    column-gap: 20px;
    row-gap: 10px;
  }
  .item-container {
    background: grey;
    width: 100%;
    height: 500px;
    margin: 10px auto;
  }
</style>