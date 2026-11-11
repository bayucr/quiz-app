<script>
  let { question, number, total, score, onanswer, onnext, ontimeout } =
    $props();

  const TIME_LIMIT = 60;

  let selected = $state(null);
  let timeLeft = $state(TIME_LIMIT);
  let answered = $derived(selected !== null);

  $effect(() => {
    if (answered) return;

    const id = setInterval(() => {
      timeLeft--;
      if (timeLeft <= 0) {
        clearInterval(id);
        ontimeout();
      }
    }, 1000);

    return () => clearInterval(id);
  });

  function choose(index) {
    if (answered) return;
    selected = index;
    onanswer(index);
  }
</script>

<div
  class="progress"
  role="progressbar"
  aria-valuemin="1"
  aria-valuemax={total}
  aria-valuenow={number}
>
  <div class="bar" style:width="{(number / total) * 100}%"></div>
</div>

<div class="top">
  <span class="muted">Soal {number} dari {total}</span>
  <span class="timer" class:danger={timeLeft <= 10}
    >Waktu: {timeLeft} detik</span
  >
</div>

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
  <button class="primary" onclick={onnext}>
    {number === total ? "Lihat hasil" : "Berikutnya"}
  </button>
{/if}

<p class="score">Skor: {score}</p>

<style>
  .progress {
    height: 8px;
    margin-bottom: 1rem;
    background: var(--border);
    border-radius: 999px;
    overflow: hidden;
  }

  .bar {
    height: 100%;
    background: var(--primary);
    transition: width 0.3s;
  }

  .top {
    display: flex;
    justify-content: space-between;
    gap: 0.5rem;
    font-size: 0.9rem;
  }

  .muted {
    color: var(--muted);
  }

  .timer {
    font-weight: 600;
  }

  .danger {
    color: var(--wrong);
  }

  .options {
    display: flex;
    flex-direction: column;
    gap: 0.6rem;
    margin: 1.25rem 0;
  }

  .options button {
    text-align: left;
  }

  .options button:disabled:not(.correct):not(.wrong) {
    opacity: 0.55;
  }

  .correct,
  .wrong {
    color: white;
    border-color: transparent;
  }

  .correct {
    background: var(--correct);
  }

  .wrong {
    background: var(--wrong);
  }

  .explanation {
    margin: 0 0 1rem;
    padding: 0.75rem 1rem;
    border-left: 4px solid var(--primary);
    background: var(--bg);
    border-radius: 6px;
  }

  .score {
    margin: 1rem 0 0;
    color: var(--muted);
    font-size: 0.9rem;
  }
</style>
