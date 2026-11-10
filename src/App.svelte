<script>
  import questions from "./lib/questions.json";

  // STATE: data yang berubah selama quiz berjalan
  let screen = $state("start");
  let currentIndex = $state(0);
  let score = $state(0);

  // DERIVED: nilai yang dihitung dari state lain
  let currentQuestion = $derived(questions[currentIndex]);

  // FUNGSI: mengubah state
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
    <h1>Quiz Svelte</h1>
    <p>{questions.length} soal tentang Svelte 5.</p>
    <button onclick={startQuiz}>Mulai</button>
  {:else if screen === "quiz"}
    <p>Soal {currentIndex + 1} dari {questions.length}</p>
    <h2>{currentQuestion.question}</h2>
    <p>Skor: {score}</p>

    <!-- tombol sementara, hanya untuk mencoba state -->
    <button onclick={() => score++}>Tambah skor (tes)</button>
    <button onclick={nextQuestion}>Berikutnya</button>
  {:else}
    <h1>Selesai!</h1>
    <p>Skor akhir: {score}</p>
    <button onclick={restart}>Ulangi</button>
  {/if}
</main>

<style>
  main {
    max-width: 520px;
    margin: 3rem auto;
    text-align: center;
  }

  button {
    margin: 0.25rem;
  }
</style>
