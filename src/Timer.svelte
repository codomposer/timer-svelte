<script>
  import Letter from './Letter.svelte';

  export let value
</script>

<Letter value={value?.charAt(0)} />
<Letter value={value?.charAt(1)} />
