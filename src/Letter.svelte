<script>
  import { withPrevious } from "svelte-previous"

  export let value

  const [current, previous] = withPrevious(0)
  $: $current = value

  let different = false
  $: if (Number($previous) !== Number($current)) {
    different = true
  }
  $: console.log(different)
</script>

{#if different}
  <div class="wrapper">
    <div class={`letter ${different && "sweep"}`}>
      <span class="top">{$previous}</span>
      <span class="down">{$current}</span>
    </div>
  </div>
{:else}
  <span class="block">{$current}</span>
{/if}

<style>
  span {
    font-size: 3rem;
    color: white;
  }

  .letter span {
    font-size: 3rem;
    line-height: 3rem;
    color: white;
  }

  .block {
    width: 40px;
    height: 60px;
    border-radius: 10px;
    background-color: #ffffff23;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .wrapper {
    position: relative;
    width: 40px;
    height: 60px;
    border-radius: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow-y: hidden;
    background-color: #ffffff23;
  }

  .letter {
    position: absolute;
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  .sweep {
    animation: sweep 1s ease-out infinite;
  }

  @keyframes sweep {
    0% {
      opacity: 1;
      transform: translateY(0px);
    }
    100% {
      opacity: 1;
      transform: translateY(-25px);
    }
  }
</style>
