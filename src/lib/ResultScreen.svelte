<script>
  let { score, total, questions, answers, onrestart } = $props();

  let percent = $derived(Math.round((score / total) * 100));
</script>

<h1>Selesai!</h1>
<p class="score">{score} dari {total} benar ({percent}%)</p>
<button onclick={onrestart}>Ulangi quiz</button>

<h2>Rekap jawaban</h2>
<ul class="recap">
  {#each questions as q, i}
    <li class={answers[i].isCorrect ? "ok" : "bad"}>
      <strong>{i + 1}. {q.question}</strong>
      <span>Jawabanmu: {q.options[answers[i].selected]}</span>
      {#if !answers[i].isCorrect}
        <span>Jawaban benar: {q.options[q.answer]}</span>
      {/if}
    </li>
  {/each}
</ul>

<style>
  .score {
    font-size: 1.25rem;
  }

  .recap {
    list-style: none;
    padding: 0;
    text-align: left;
  }

  .recap li {
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
    margin: 0.75rem 0;
    padding: 0.75rem;
    border-left: 4px solid;
    border-radius: 4px;
  }

  .ok {
    border-color: #2e9e5b;
  }

  .bad {
    border-color: #d64545;
  }
</style>
