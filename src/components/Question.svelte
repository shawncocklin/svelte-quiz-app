<script>
  export let question
  export let nextQuestion
  export let updateScore

  let answers = question.incorrect_answers.map((answer) => {
    return {
      answer: answer,
      correct: false,
    }
  })
  let correctAnswer = question.correct_answer
  let isCorrect
  let isAnswered = false

  let allAnswers = [
    ...answers,
    {
      answer: correctAnswer,
      correct: true,
    },
  ]

  shuffle(allAnswers)

  function shuffle(array) {
    array.sort(() => Math.random() - 0.5)
  }

  function checkQuestion(correct) {
    if (!isAnswered) {
      isCorrect = correct
      isAnswered = true
      if (correct === true) {
        updateScore()
      }
    }
  }
</script>

<h3>{@html question.question}</h3>

{#each allAnswers as answer}
  <button on:click={() => checkQuestion(answer.correct)}>{@html answer.answer}</button>
{/each}

{#if isAnswered}
  <h4>
    {#if isCorrect}
      Correct!
    {:else}
      Whoopsie!
    {/if}
  </h4>
{/if}

<div><button on:click={nextQuestion}>Next Question</button></div>

<style>
</style>
