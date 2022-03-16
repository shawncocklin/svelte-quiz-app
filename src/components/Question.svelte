<script>
  import { score } from '../Store.js'
  export let question
  export let nextQuestion
  //#region variables
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
  //#endregion

  shuffle(allAnswers)

  function shuffle(array) {
    array.sort(() => Math.random() - 0.5)
  }

  function checkQuestion(correct) {
    if (!isAnswered) {
      isCorrect = correct
      isAnswered = true
      if (correct === true) {
        score.update((val) => {
          return val + 1
        })
      }
    }
  }
</script>

<h3>{@html question.question}</h3>

{#each allAnswers as answer}
  <button on:click={() => checkQuestion(answer.correct)}>{@html answer.answer}</button>
{/each}

{#if isAnswered}
  <h4 class:correct={isCorrect} class:wrong={!isCorrect}>
    {#if isCorrect}
      Correct!
    {:else}
      Whoopsie!
    {/if}
  </h4>
{/if}

<div><button disabled={!isAnswered} on:click={nextQuestion}>Next Question</button></div>

<style>
  .wrong {
    color: red;
  }
  .correct {
    color: green;
  }
</style>
