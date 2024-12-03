<script>
  import CountdownTimer from './CountdownTimer.svelte';
  let theme = "light";

  function toggleTheme() {
    theme = theme === "light" ? "dark" : "light";
    document.body.dataset.theme = theme;
  }
</script>

<main>
  <h1>Brevis AI Release</h1>
  <button on:click={toggleTheme}>Toggle Theme</button>
  <CountdownTimer />
</main>
