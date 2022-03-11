<script>
  import Button from './Button.svelte'
  let answers = ['a', 'b', 'c', 'd']
</script>

<div>
  {#each answers as answer}
    <Button selectedAnswer={answer} />
  {/each}
</div>
