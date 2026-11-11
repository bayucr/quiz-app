<script>
  let { score, total, questions, answers, onrestart } = $props();

  let percent = $derived(Math.round((score / total) * 100));
</script>

<div class="summary">
  <h1>Selesai!</h1>
  <p class="big">{score} dari {total} benar</p>
  <p class="muted">{percent}%</p>
  <button class="primary" onclick={onrestart}>Ulangi quiz</button>
</div>

<h2>Rekap jawaban</h2>
<ul class="recap">
  {#each questions as q, i}
    <li class={answers[i].isCorrect ? "ok" : "bad"}>
      <strong>{i + 1}. {q.question}</strong>
      <span>
        Jawabanmu:
        {answers[i].selected === null
          ? "Waktu habis"
          : q.options[answers[i].selected]}
      </span>
      {#if !answers[i].isCorrect}
        <span>Jawaban benar: {q.options[q.answer]}</span>
      {/if}
    </li>
  {/each}
</ul>

<style>
  .summary {
    text-align: center;
    margin-bottom: 1.5rem;
  }

  .big {
    margin: 0;
    font-size: 1.5rem;
    font-weight: 700;
  }

  .muted {
    margin: 0 0 1rem;
    color: var(--muted);
  }

  .recap {
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .recap li {
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
    margin: 0.75rem 0;
    padding: 0.75rem 1rem;
    background: var(--bg);
    border-left: 4px solid;
    border-radius: 6px;
  }

  .ok {
    border-color: var(--correct);
  }

  .bad {
    border-color: var(--wrong);
  }
</style>
