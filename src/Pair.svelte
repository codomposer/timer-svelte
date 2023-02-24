<script>
  import Letter from "./Letter.svelte"

  export let value
  export let max
  export let key
</script>

<Letter value={value?.charAt(0)} max={max?.charAt(0)} key={key?.charAt(0)} />
<Letter value={value?.charAt(1)} max={max?.charAt(1)} key={key?.charAt(1)} />
