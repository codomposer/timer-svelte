<script>
  import { onMount, onDestroy } from "svelte"
  import { withPrevious } from "svelte-previous"

  import Swiper from "swiper"
  import "swiper/swiper-bundle.css"

  export let value
  export let max
  export let key

  const [current, previous] = withPrevious(0)
  $: $current = value

  let different = false
  let items = []
  let swiper
  let xx = value === "0" ? 1 : 2

  for (let i = 0; i <= Number(max); i++) {
    items.push((Number(max) + xx + Number(value) - i) % (Number(max) + 1))
  }

  console.log(items)
  onMount(() => {
    swiper = new Swiper(`.${key}-mySwiper`, {
      slidesPerView: 1,
      direction: "vertical",
      loop: true,
    })
  })

  $: if (Number($previous) !== Number($current)) {
    different = true
    swiper?.slideNext()
  }
</script>

<div class="container">
  <div class={`swiper ${key}-mySwiper`}>
    <div class="swiper-wrapper">
      <!-- Your slides here -->
      {#each items as item}
        <div class="swiper-slide">
          {item}
        </div>
      {/each}
    </div>
  </div>
</div>

<style>
  .container {
    position: relative;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    /* overflow-y: hidden; */
  }
  .swiper {
    width: 40px;
    height: 60px;
    border-radius: 10px;
    background-color: #ffffff23;
  }
  .swiper-slide {
    text-align: center;
    font-size: 18px;
    background-color: #ffffff23;
    font-size: 2rem;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
