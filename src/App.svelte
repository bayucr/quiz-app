<script>
  import questions from "./lib/questions.json";
  let nama = $state("Pelajar");
  let klik = $state(0);
</script>

<main>
  <h1>Halo, {nama}!</h1>
  <p>Ini calon quiz app-ku.</p>

  <input bind:value={nama} placeholder="Ketik namamu" />

  <button onclick={() => klik++}>Diklik {klik} kali</button>

  <p>{questions[0].question}</p>
  <p>Jumlah soal: {questions.length}</p>
</main>

<style>
  main {
    max-width: 480px;
    margin: 3rem auto;
    text-align: center;
  }
</style>
