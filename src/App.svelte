<script>
  import { onMount, onDestroy } from 'svelte';

	import Time from './Timer.svelte';

  let interval;
  let time = 0;
	let days = '00';
	let hours = '00';
	let minutes = '00';
	let seconds = '00';


  function startTimer() {
    interval = setInterval(() => {
      time++;
			days = Math.floor(time / 216000).toString().padStart(2, '0');
			hours = Math.floor(time / 3600).toString().padStart(2, '0');
			minutes = Math.floor(time / 60).toString().padStart(2, '0');
			seconds = (time % 60).toString().padStart(2, '0');
    }, 1000);
  }

  function stopTimer() {
    clearInterval(interval);
    interval = null;
  }

  function resetTimer() {
    time = 0;
  }

  onMount(() => {
    startTimer();
  });

  onDestroy(() => {
    stopTimer();
  });
</script>

<div class="timer">
	<div class="time">
		<Time value={days} />
		<span class="dot">:</span>
		<Time value={hours} />
		<span class="dot">:</span>
		<Time value={minutes} />
		<span class="dot">:</span>
		<Time value={seconds} />
	</div>
  <div class="buttons">
    {#if interval}
      <button on:click={stopTimer}>Stop</button>
    {:else}
      <button on:click={startTimer}>Start</button>
    {/if}
    <button on:click={resetTimer}>Reset</button>
  </div>
</div>

<style>
  .timer {
		padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
		background-color: rgba(60, 60, 151, 0.966);
  }

	.time {
		display: flex;
		gap: 4px;
	}

  .timer span {
    font-size: 3rem;
		line-height: 3rem;
		color: white;
  }

  .timer .buttons {
		margin-top: 20px;
    display: flex;
    gap: 1rem;
  }

  .timer button {
    font-size: 1.2rem;
    padding: 0.5rem 1rem;
  }

	.dot {
		margin: 0px 8px 0px 8px;
	}
</style>