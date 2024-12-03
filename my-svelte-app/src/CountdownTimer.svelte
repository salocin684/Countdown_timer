<script>
  import { onMount } from "svelte";

  let targetDate = new Date("2024-12-04T23:59:59").getTime();
  let timeDisplay = "";
  let isAfterTarget = false;

  const calculateTimeLeft = () => {
    const now = new Date().getTime();
    const difference = targetDate - now;

    let totalSeconds = Math.abs(difference) / 1000; // Absolute tijd in seconden
    const days = Math.floor(totalSeconds / (24 * 3600));
    totalSeconds %= 24 * 3600;
    const hours = Math.floor(totalSeconds / 3600);
    totalSeconds %= 3600;
    const minutes = Math.floor(totalSeconds / 60);
    const seconds = Math.floor(totalSeconds % 60);

    isAfterTarget = difference < 0;

    // Maak de tijdweergave
    if (days > 0) {
      timeDisplay = `${isAfterTarget ? "T+" : "T-"}${days}:${String(hours).padStart(2, "0")}:${String(minutes).padStart(2, "0")}:${String(seconds).padStart(2, "0")}`;
    } else {
      timeDisplay = `${isAfterTarget ? "T+" : "T-"}${String(hours).padStart(2, "0")}:${String(minutes).padStart(2, "0")}:${String(seconds).padStart(2, "0")}`;
    }
  };

  onMount(() => {
    calculateTimeLeft();
    const interval = setInterval(calculateTimeLeft, 1000);
    return () => clearInterval(interval);
  });
</script>

<div id="app">
  <h1>{timeDisplay}</h1>
</div>

<style>
  #app {
    text-align: center;
    padding: 2rem;
    border-radius: 1rem;
    background: rgba(0, 0, 0, 0.7);
    color: hsl(var(--foreground));
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  }

  h1 {
    font-size: 2rem;
    color: hsl(var(--accent));
    text-shadow: 0 0 10px hsl(var(--accent)), 0 0 20px hsl(var(--accent));
  }

  @media (min-width: 768px) {
    h1 {
      font-size: 3rem;
    }
  }
</style>
