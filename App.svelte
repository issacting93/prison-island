<script>
	import Button from "./Button.svelte";
	import { onMount } from "svelte";
	import ChooseCharacterPage from "./Templates/ChooseCharacterPage.svelte";
	import Flipbook from "./Templates/Flipbook.svelte";
	import Transition from "./Templates/Transition.svelte";
	import RoleIndicator from "./Templates/RoleIndicator.svelte";
	import ItemDetails from "./Templates/ItemDetails.svelte";
	import EscapeChoice from "./Templates/EscapeChoice.svelte";
	import Biography from "./Templates/Biography.svelte";
	import jQuery from "jquery";
	import stages from "./data.json";
	let state = "start";
	let count = 0;
	let role;
	let selectedRole;
	let currentStage = stages[count].type;
	let selectedPage;
	import AudioPlayer, { stopAll } from "./AudioPlayer.svelte";

	let audioTracks = ["https://sveltejs.github.io/assets/music/strauss.mp3"];
	function handleClick() {
	  count += 1;
	  if (count >= 5) {
	    count = 0;
	  }
	}
	onMount(() => {
	  window.jQuery = jQuery;
	});
</script>

<main>  

<button on:click={stopAll}>
  Mute Audio
</button>

{#each audioTracks as src}
  <AudioPlayer {src} />
{/each}
<div class="role-container">
{count} 
{#if selectedRole == undefined}
-
{:else}
	<RoleIndicator role={selectedRole}/>
{/if}
	
</div>

	{#if stages[count].type == "ChooseCharacterPage" }
	<ChooseCharacterPage bind:inputSelectedRole={selectedRole} bind:count={count}  bind:selectedPage = {selectedPage} />
		{:else if stages[count].type == "ItemDetails" }
	<ItemDetails bind:count={count} role={selectedRole}  bind:selectedPage = {selectedPage}/>
	{:else if stages[count].type == "Transition"}
	<Transition bind:count={count}  bind:selectedPage = {selectedPage} />
		{:else if stages[count].type == "EscapeChoice"}
	<EscapeChoice bind:count={count}  bind:selectedPage = {selectedPage}/>	
	{:else}
	<Biography bind:count={count}  />

{/if}

</main>	
	 

<style>
  main {
    font-family: sans-serif;
    text-align: center;
    background: black;
  }

  .role-container {
    position: fixed;
    left: 0px;
  }
</style>
