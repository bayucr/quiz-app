<script>
  import questions from "./lib/questions.json";
  import StartScreen from "./lib/StartScreen.svelte";
  import QuestionCard from "./lib/QuestionCard.svelte";
  import ResultScreen from "./lib/ResultScreen.svelte";

  let screen = $state("start");
  let currentIndex = $state(0);
  let score = $state(0);
  let answers = $state([]);

  let currentQuestion = $derived(questions[currentIndex]);

  function startQuiz() {
    currentIndex = 0;
    score = 0;
    answers = [];
    screen = "quiz";
  }

  function handleAnswer(selectedIndex) {
    const isCorrect = selectedIndex === currentQuestion.answer;
    if (isCorrect) score++;
    answers.push({ selected: selectedIndex, isCorrect });
  }

  function handleTimeout() {
    score = Math.max(0, score - 1);
    answers.push({ selected: null, isCorrect: false });
    nextQuestion();
  }

  function nextQuestion() {
    if (currentIndex < questions.length - 1) {
      currentIndex++;
    } else {
      screen = "result";
    }
  }
</script>

<main>
  <div class="card">
    {#if screen === "start"}
      <StartScreen total={questions.length} onstart={startQuiz} />
    {:else if screen === "quiz"}
      {#key currentIndex}
        <QuestionCard
          question={currentQuestion}
          number={currentIndex + 1}
          total={questions.length}
          {score}
          onanswer={handleAnswer}
          onnext={nextQuestion}
          ontimeout={handleTimeout}
        />
      {/key}
    {:else}
      <ResultScreen
        {score}
        total={questions.length}
        {questions}
        {answers}
        onrestart={startQuiz}
      />
    {/if}
  </div>
</main>

<style>
  main {
    max-width: 600px;
    margin: 0 auto;
    padding: 1rem;
  }

  .card {
    margin-top: 1.5rem;
    padding: 1.5rem;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    box-shadow: 0 4px 16px rgb(0 0 0 / 0.06);
  }

  @media (max-width: 480px) {
    main {
      padding: 0.5rem;
    }

    .card {
      margin-top: 0.5rem;
      padding: 1rem;
    }
  }
</style>
