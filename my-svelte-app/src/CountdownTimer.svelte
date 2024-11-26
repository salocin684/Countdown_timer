<script>
  import { onMount } from "svelte";

  let targetDate = new Date("2024-11-30T23:59:59").getTime();
  let timeLeft = {};

  const calculateTimeLeft = () => {
    const now = new Date().getTime();
    const difference = targetDate - now;

    timeLeft = difference > 0
      ? {
          days: Math.floor(difference / (1000 * 60 * 60 * 24)),
          hours: Math.floor((difference / (1000 * 60 * 60)) % 24),
          minutes: Math.floor((difference / (1000 * 60)) % 60),
          seconds: Math.floor((difference / 1000) % 60),
        }
      : { days: 0, hours: 0, minutes: 0, seconds: 0 };
  };

  onMount(() => {
    calculateTimeLeft();
    const interval = setInterval(calculateTimeLeft, 1000);
    return () => clearInterval(interval);
  });
</script>

<div class="time">
  <p><i class="fas fa-calendar-day"></i> {timeLeft.days} Days</p>
  <p><i class="fas fa-clock"></i> {timeLeft.hours} Hours</p>
  <p><i class="fas fa-stopwatch"></i> {timeLeft.minutes} Minutes</p>
  <p><i class="fas fa-hourglass-end"></i> {timeLeft.seconds} Seconds</p>
</div>

<style>
  .timer {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1.5rem;
    text-transform: uppercase;
    font-weight: bold;
  }

  .time {
    display: flex;
    gap: 2rem;
    font-size: 1.5rem;
    color: hsl(var(--accent));
  }

  .time p {
    text-align: center;
    background: rgba(255, 255, 255, 0.1);
    padding: 0.5rem 1rem;
    border-radius: 0.5rem;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  }
</style>