<script>
  import { fade, fly } from "svelte/transition";
  import { cubicOut } from "svelte/easing";

  export let key;
</script>

<div
  in:fly={{ y: 20, duration: 300, delay: 300, easing: cubicOut }}
  out:fade={{ duration: 200 }}
>
  <slot />
</div>
