<script>
  import { onMount, onDestroy } from "svelte";
  import { fade, scale } from "svelte/transition";
  import FeedbackItem from "./FeedbackItem.svelte";
  import { FeedbackStore } from "../stores";
  // stores, the long way

  // let feedback = [];

  // const unsubscribe = FeedbackStore.subscribe((data) => (feedback = data));

  // onMount(() => {
  //   console.log("FeedbackList mounted");
  // });

  // onDestroy(() => {
  //   unsubscribe();
  // });
</script>

{#each $FeedbackStore as fb (fb.id)}
  <div in:scale out:fade={{ duration: 500 }}>
    <FeedbackItem item={fb} />
  </div>
{/each}
