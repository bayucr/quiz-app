<script>
  import questions from "./lib/questions.json";
  import StartScreen from "./lib/StartScreen.svelte";
  import QuestionCard from "./lib/QuestionCard.svelte";
  import ResultScreen from "./lib/ResultScreen.svelte";

  let screen = $state("start");
  let currentIndex = $state(0);
  let score = $state(0);

  let currentQuestion = $derived(questions[currentIndex]);

  function startQuiz() {
    currentIndex = 0;
    score = 0;
    screen = "quiz";
  }

  function nextQuestion() {
    if (currentIndex < questions.length - 1) {
      currentIndex++;
    } else {
      screen = "result";
    }
  }

  function restart() {
    screen = "start";
  }
</script>

<main>
  {#if screen === "start"}
    <StartScreen total={questions.length} onstart={startQuiz} />
  {:else if screen === "quiz"}
    <QuestionCard
      question={currentQuestion}
      number={currentIndex + 1}
      total={questions.length}
      {score}
      onnext={nextQuestion}
    />
  {:else}
    <ResultScreen {score} total={questions.length} onrestart={restart} />
  {/if}
</main>

<style>
  main {
    max-width: 520px;
    margin: 3rem auto;
    text-align: center;
  }
</style>
