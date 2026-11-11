<script>
  let { question, number, total, score, onanswer, onnext, ontimeout } =
    $props();

  const TIME_LIMIT = 60;

  let selected = $state(null);
  let timeLeft = $state(TIME_LIMIT);
  let answered = $derived(selected !== null);

  // EFFECT: menjalankan timer, berhenti saat soal sudah dijawab
  $effect(() => {
    if (answered) return;

    const id = setInterval(() => {
      timeLeft--;
      if (timeLeft <= 0) {
        clearInterval(id);
        ontimeout();
      }
    }, 1000);

    // fungsi pembersih: dijalankan saat effect berhenti atau komponen dihapus
    return () => clearInterval(id);
  });

  function choose(index) {
    if (answered) return;
    selected = index;
    onanswer(index);
  }
</script>

<p>Soal {number} dari {total}</p>
<p class="timer" class:danger={timeLeft <= 10}>Waktu: {timeLeft} detik</p>
<h2>{question.question}</h2>

<div class="options">
  {#each question.options as option, i}
    <button
      class:correct={answered && i === question.answer}
      class:wrong={answered && i === selected && i !== question.answer}
      disabled={answered}
      onclick={() => choose(i)}
    >
      {option}
    </button>
  {/each}
</div>

{#if answered}
  <p class="explanation">{question.explanation}</p>
  <button onclick={onnext}>
    {number === total ? "Lihat hasil" : "Berikutnya"}
  </button>
{/if}

<p>Skor: {score}</p>

<style>
  .timer {
    font-weight: bold;
  }

  .danger {
    color: #d64545;
  }

  .options {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin: 1rem 0;
  }

  .correct {
    background: #2e9e5b;
    color: white;
  }

  .wrong {
    background: #d64545;
    color: white;
  }

  .explanation {
    margin: 1rem 0;
    font-style: italic;
  }
</style>
