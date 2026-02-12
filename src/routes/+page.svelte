<script lang="ts">
  const eightyeightthirtyones = [
    "nocookie.gif",
    "nyaabanner.gif",
    "vscbutton.gif"
  ]
</script>

<h1>test</h1>
<div class="badges">
  {#each eightyeightthirtyones as img}
    <img src={`/88x31/${img}`} alt={img} />
  {/each}
</div>

<style>
  .badges {
    display: grid;
    grid-template-columns: auto auto auto;
    padding: 10px;
  }
</style>