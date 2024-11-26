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

<div class="timer">
  <h1>Countdown Timer</h1>
  <div class="time">
    <p>{timeLeft.days} Days</p>
    <p>{timeLeft.hours} Hours</p>
    <p>{timeLeft.minutes} Minutes</p>
    <p>{timeLeft.seconds} Seconds</p>
  </div>
</div>
