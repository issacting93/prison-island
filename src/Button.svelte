<script>
	export let count = 0;

	function handleClick() {
	  count += 1;
	}
</script>

<style>
		button {
		  background-image: url(Images/Button.svg);
		  background-size: contain;
		  border: 0px solid white;
		  background-repeat: no-repeat;
		  color: white;
		  background-position: center;
		  padding: 8px;
		  background-color: #101010;
		  margin: 12px;
		  transition: 0.2s all;
		}

		button:hover {
		  opacity: 0.3;
		}
</style>

<button on:click={handleClick}>
 Count {count} {count === 1 ? 'time' : 'times'}
</button>