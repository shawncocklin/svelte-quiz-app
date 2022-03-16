<script>
  import { fade, fly } from 'svelte/transition'
  import Question from './Question.svelte'
  import Modal from './Modal.svelte'
  import { score } from '../Store.js'

  const ENDPOINT = 'https://opentdb.com/api.php?amount=10&category=22&type=multiple'
  const winScore = 1

  //#region variables
  let quiz = getQuiz()
  let activeQuestion = 0
  let openModal = false
  //#endregion

  //#region functions
  async function getQuiz() {
    const res = await fetch(ENDPOINT)
    const quiz = await res.json()
    return quiz
  }

  function nextQuestion() {
    activeQuestion += 1
  }

  function resetQuiz() {
    score.set(0)
    quiz = getQuiz()
    activeQuestion = 0
    openModal = false
  }

  //#endregion

  // reactive syntax

  //TODO: add logic to open modal when quiz is done and display win or lose depending on the score
  $: if ($score >= winScore && questionNumber > 10) {
    openModal = true
  }

  $: questionNumber = activeQuestion + 1
</script>

<!-- #region markup -->
<div>
  <button on:click={resetQuiz}>Start Quiz</button>

  <h3>Score: {$score}</h3>
  <h4>Question #{questionNumber}</h4>

  {#await quiz}
    loading...
  {:then data}
    {#each data.results as question, index}
      {#if index === activeQuestion}
        <div in:fly={{ x: 100 }} out:fade class="fade-wrapper">
          <Question {nextQuestion} {question} />
        </div>
      {/if}
    {/each}
  {/await}
</div>

{#if openModal}
  <Modal on:close={resetQuiz}>
    <h2>You Win!</h2>
    <p>Score: {$score}/10</p>
    <p>Congratulations</p>
    <button on:click={resetQuiz}>Play Again</button>
  </Modal>
{/if}

<!-- #endregion -->
<style>
  .fade-wrapper {
    position: absolute;
  }
</style>
