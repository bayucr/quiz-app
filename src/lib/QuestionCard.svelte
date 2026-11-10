<script>
  let { question, number, total, score, onnext } = $props();
</script>

<p>Soal {number} dari {total}</p>
<h2>{question.question}</h2>

<div class="options">
  {#each question.options as option}
    <button>{option}</button>
  {/each}
</div>

<p>Skor: {score}</p>
<button onclick={onnext}>Berikutnya</button>

<style>
  .options {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin: 1rem 0;
  }
</style>
