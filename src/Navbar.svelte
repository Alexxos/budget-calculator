<script>
  export let showForm;
</script>

<style>
  nav {
    background-color: var(--primaryColor);
  }
</style>

<nav class="nav">
  <div class="nav-center">
    <h1 class="nav-title">Budget Calculator</h1>

    <button class="nav-btn" on:click={showForm}>
    <i class="far fa-plus-square" aria-hidden="true"></i>
      add item
    </button>
  </div>
</nav>
