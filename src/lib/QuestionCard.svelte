<script>
  let { question, number, total, score, onanswer, onnext } = $props();

  // STATE LOKAL: hanya kartu ini yang butuh tahu pilihan pemain
  let selected = $state(null);
  let answered = $derived(selected !== null);

  function choose(index) {
    if (answered) return;
    selected = index;
    onanswer(index); // sebelumnya: onanswer(index === question.answer)
  }
</script>

<p>Soal {number} dari {total}</p>
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
