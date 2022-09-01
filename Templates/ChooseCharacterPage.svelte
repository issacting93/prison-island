<script>
	import { createEventDispatcher } from "svelte";
	const dispatch = createEventDispatcher();
	export let count = 0;
	export let inputSelectedRole;
	function handleClick(role) {
	  count += 1;
	  inputSelectedRole = role;
	}
</script>

<style>
	.img {
	  height: 80vh;
	  background: #f7f7f7;
	  border: 1px black solid;
	}
	.main-container {
	  display: flex;
	  width: 100%;
	  justify-content: center;
	}
	.card-container {
	  display: flex;
	  flex-direction: column;
	  min-width: 500px;
	}
</style>

<div >
Select a role : {inputSelectedRole}
<div class="main-container">

<div class="card-container"> 
  <div class="img">
  </div>
   <button  on:click={() => handleClick("Warden")} >
	  Warden
</button>
</div>

<div class="card-container"> 
  <div class="img">
  </div>
<button  on:click={() => handleClick("Prisoner")}  >
 Prisoner
</button>
</div>
</div>
 

</div>
