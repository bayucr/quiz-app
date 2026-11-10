<script>
  let { total, onstart } = $props();
</script>

<h1>Quiz Svelte</h1>
<p>{total} soal tentang Svelte 5.</p>
<button onclick={onstart}>Mulai</button>
