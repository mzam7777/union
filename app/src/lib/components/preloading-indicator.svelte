<script lang="ts">
import { onMount } from "svelte"
import { cn } from "$lib/utilities/shadcn.ts"

let [progress, visible] = [0, false]
onMount(() => {
  visible = true
  const next = () => {
    progress += 0.1
    const remaining = 1 - progress
    if (remaining > 0.15) setTimeout(next, 500 / remaining)
  }
  setTimeout(next, 250)
})
</script>

{#if visible}
  <div class="absolute w-full h-1 z-[999] left-0 top-0">
    <div
      style="width: {progress * 100}%"
      class={cn(['absolute h-full bg-union-accent-600 transition-[width] duration-500 left-0 top-0'])}
    />
  </div>
{/if}

{#if progress >= 0.4}
  <div
    class="fixed size-full bg-[rgba(234,248,255,0.04)] pointer-events-none z-[998] animate-[fade_0.4s]"
  />
{/if}

<style lang="postcss">
  @keyframes fade {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
</style>
