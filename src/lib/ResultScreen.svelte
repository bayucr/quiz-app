<script>
  let { score, total, onrestart } = $props();
</script>

<h1>Selesai!</h1>
<p>Skor akhir: {score} dari {total}</p>
<button onclick={onrestart}>Ulangi</button>
