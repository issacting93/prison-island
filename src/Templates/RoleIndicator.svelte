<script>
  export let role;

  import utility from "../util.json";
</script>

<div>
  {#if role == "Warden"}
    <div
      class="role-container thumbnailW"
      style="background-image:{utility[0].wardenThumbnail}"
    />
  {:else}
    <div
      class="role-container thumbnailP"
      style="background-image:{utility[0].prisonerThumbnail}"
    />
  {/if}
</div>

<style>
  div#preload {
    display: none;
  }
  .role-container {
    margin: 40px;
    top: 10px;
    left: 10px;
    padding: 20px;
    border-radius: 200px;
    background: white;
    position: absolute;
    z-index: 11;
    background-size: cover;
    position: fixed;
    left: 0px;
    height: 40px;
    width: 40px;
    z-index: 11;
  }

  .thumbnailP {
    background-image: url(Images/Prisoner_thumbnail.png);
  }

  .thumbnailW {
    background-image: url(Images/Warden_thumbnail.png);
  }
</style>
