<script>
  export let selectedAnswer
  let result = ''
  let correctAnswer = 'b'
  function pickAnswer(answer) {
    if (answer == correctAnswer) {
      return (result = 'Correct')
    }
    result = 'whOOPSIE'
  }
</script>

{#if result}
  <h4>{result}</h4>
{:else}
  <h5>Pick and answer</h5>
{/if}

<button on:click={() => pickAnswer(selectedAnswer)}
  >Answer {selectedAnswer}</button
>
