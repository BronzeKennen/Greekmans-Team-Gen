<script>
  import Players from './lib/Players.svelte'
  import Wheel from './lib/Wheel.svelte'
</script>

<main>
  <div class="main-header">
    <Players/>
    <Wheel/>
  </div>
</main>

<style>
  .main-header {
    display:grid;
    grid-template-columns: 1fr 1fr;
  }

</style>
