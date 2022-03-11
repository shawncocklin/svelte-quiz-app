<script>
  const ENDPOINT =
    'https://opentdb.com/api.php?amount=10&category=22&type=multiple'
  let correctAnswer = 'b'
  let answers = ['a', 'b', 'c', 'd']

  let quiz = getQuiz()

  let result = ''

  function pickAnswer(answer) {
    if (answer == correctAnswer) {
      return (result = 'Correct')
    }
    result = 'whOOPSIE'
  }

  async function getQuiz() {
    const res = await fetch(ENDPOINT)
    const quiz = await res.json()
    console.log(quiz)
    return quiz
  }

  function handleClick() {
    quiz = getQuiz()
  }
</script>

<div>
  {#if result}
    <h4>{result}</h4>
  {:else}
    <h5>Pick and answer</h5>
  {/if}

  {#await quiz}
    loading...
  {:then data}
    <h3>{data.results[0].question}</h3>
  {/await}

  <button on:click={handleClick}>Get Quiz</button>
  {#each answers as answer}
    <button on:click={() => pickAnswer(answer)}>Answer {answer}</button>
  {/each}
</div>

<style></style>
