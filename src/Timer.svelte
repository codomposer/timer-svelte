<script>
  import { onMount, onDestroy } from 'svelte';

	import Pair from './Pair.svelte';

  let interval;
  export let time;
  
  let temp = time;
	let days = Math.floor(temp / 86400).toString().padStart(2, '0');
  temp %= (3600 * 24);
	let hours = Math.floor(temp / 3600).toString().padStart(2, '0');
  temp %= 3600;
	let minutes = Math.floor(temp / 60).toString().padStart(2, '0');
	let seconds = (temp % 60).toString().padStart(2, '0');

  console.log({days, hours, minutes, seconds})

  function startTimer() {
    interval = setInterval(() => {
      time--;
      formatSeconds(time)
    }, 1000);
  }

  function formatSeconds(downSeconds) {
    days = Math.floor(downSeconds / (3600 * 24)).toString().padStart(2, '0');
    downSeconds %= (3600 * 24);
    hours = Math.floor(downSeconds / 3600).toString().padStart(2, '0');
    downSeconds %= 3600;
    minutes = Math.floor(downSeconds / 60).toString().padStart(2, '0');
    seconds = (downSeconds %= 60).toString().padStart(2, '0');  
  }

  function stopTimer() {
    clearInterval(interval);
    interval = null;
  }

  onMount(() => {
    startTimer();
  });

  onDestroy(() => {
    stopTimer();
    time = 0;
  });

</script>

<div class="timer">
	<div class="time">
		<Pair value={days} max={"39"} key={"Dd"} />
		<span class="dot">:</span>
		<Pair value={hours} max={"29"} key={"Hh"} />
		<span class="dot">:</span>
		<Pair value={minutes} max={"59"} key={"Mm"} />
		<span class="dot">:</span>
		<Pair value={seconds} max={"59"} key={"Ss"} />
	</div>
  <div class="buttons">
    {#if interval}
      <button on:click={stopTimer}>Stop</button>
    {:else}
      <button on:click={startTimer}>Start</button>
    {/if}
  </div>
</div>


<style>
  .timer {
		padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
		background-color: rgba(53, 53, 184, 0.966);
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