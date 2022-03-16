<script>
  import { fade, fly } from 'svelte/transition'
  import { createEventDispatcher } from 'svelte'

  const dispatch = createEventDispatcher()
</script>

<div class="modal-container" transition:fade>
  <div class="modal" transition:fly={{ y: -100 }}>
    <button
      on:click={() => {
        dispatch('close')
      }}>Close</button
    >
    <slot />
  </div>
</div>

<style>
  .modal-container {
    position: fixed;
    inset: 0;
    background-color: hsla(0, 0%, 0%, 0.8);
  }

  .modal {
    background-color: #e3e3e3;
    padding: 1.5rem;
    border-radius: 1rem;
  }
</style>
