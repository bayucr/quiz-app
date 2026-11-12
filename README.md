# Quiz Svelte

Aplikasi quiz interaktif untuk belajar Svelte 5, dibuat sebagai latihan
mempelajari Svelte dan Vite.

**Demo:** https://USERNAME.github.io/quiz-app/

## Fitur

- 10 soal pilihan ganda tentang Svelte 5
- Urutan soal diacak setiap kali quiz dimulai
- Umpan balik langsung (hijau/merah) beserta penjelasan jawaban
- Timer 60 detik per soal; skor berkurang 1 jika waktu habis
- Rekap jawaban di akhir quiz
- Tampilan responsif dan mendukung mode gelap

## Teknologi

- [Svelte 5](https://svelte.dev) (runes: `$state`, `$derived`, `$effect`, `$props`)
- [Vite](https://vite.dev)
- GitHub Actions + GitHub Pages untuk deploy

## Menjalankan di komputer sendiri

```bash
git clone https://github.com/USERNAME/quiz-app.git
cd quiz-app
npm install
npm run dev
```

## Menambah soal

Edit `src/lib/questions.json`. Format satu soal:

```json
{
  "id": 11,
  "question": "Teks pertanyaan",
  "options": ["Pilihan A", "Pilihan B", "Pilihan C", "Pilihan D"],
  "answer": 0,
  "explanation": "Penjelasan jawaban benar"
}
```

`answer` adalah nomor index (mulai dari 0) pilihan yang benar.

## Struktur

```
src/
├── App.svelte             # state utama dan alur antar layar
├── app.css                # gaya global dan variabel warna
└── lib/
    ├── StartScreen.svelte
    ├── QuestionCard.svelte
    ├── ResultScreen.svelte
    └── questions.json
```

Proyek ini mengacu pada spesifikasi [Quiz App](https://roadmap.sh/projects/quiz-app)
dari roadmap.sh.
