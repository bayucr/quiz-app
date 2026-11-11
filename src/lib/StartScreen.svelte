<script>
  let { total, onstart } = $props();
</script>

<div class="start">
  <h1>Quiz Svelte</h1>
  <p>{total} soal tentang Svelte 5. Waktu 60 detik per soal.</p>
  <button class="primary" onclick={onstart}>Mulai</button>
</div>

<style>
  .start {
    text-align: center;
    padding: 1.5rem 0;
  }

  p {
    color: var(--muted);
    margin-bottom: 1.5rem;
  }
</style>
