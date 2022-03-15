<script>
  import Question from './Question.svelte'
  const ENDPOINT = 'https://opentdb.com/api.php?amount=10&category=22&type=multiple'

  let quiz = getQuiz()
  let activeQuestion = 0
  let score = 0

  async function getQuiz() {
    const res = await fetch(ENDPOINT)
    const quiz = await res.json()
    return quiz
  }

  function nextQuestion() {
    activeQuestion += 1
  }

  function resetQuiz() {
    score = 0
    quiz = getQuiz()
    activeQuestion = 0
  }

  function updateScore() {
    score++
  }
</script>

<div>
  <button on:click={resetQuiz}>Start Quiz</button>

  <h3>Score: {score}</h3>
  <h4>Question #{activeQuestion + 1}</h4>

  {#await quiz}
    loading...
  {:then data}
    {#each data.results as question, index}
      {#if index === activeQuestion}
        <Question {nextQuestion} {question} {updateScore} />
      {/if}
    {/each}
  {/await}
</div>

<style></style>
