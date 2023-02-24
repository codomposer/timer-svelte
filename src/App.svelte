<script>
  import Timer from "./Timer.svelte"

  let time = 99992

  function resetTimer() {
    time = 100;
  }

  let time1 = 0;
  function onTimeChange(e) {
    time1 = Number(e.target.value);
    time = time1;
    console.log(time);
  }
  
</script>

<Timer time={time} />

<button on:click={resetTimer}>Reset</button>
<input type="text" value={time1} on:change={onTimeChange} />
