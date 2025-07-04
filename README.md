# belajarGitdanGitHub

dokumentasi pembelajaran git dan gitHub dari channel youtube web programming UNPAS.

motivasi utama : keberlancaran dalam pengerjaan kelompok Tugas besar

## Branching Strategy

Untuk workflow **Git** yang lebih kompleks, terutama dalam proyek berkelompok yang melibatkan banyak branch, kamu perlu memahami beberapa konsep dan praktik lanjutan agar kolaborasi tim berjalan lancar, kode tetap stabil, dan konflik bisa diminimalkan.

**1. Branching Strategy:**

- **Feature Branch Workflow:** Setiap fitur atau perbaikan dikerjakan di branch terpisah (misal: `feature/login`, `bugfix/error-404`). Ini mencegah kode yang belum stabil masuk ke branch utama.
- **Main Branches:** Biasanya ada dua branch utama:
  - **main/master:** Branch untuk kode yang sudah siap rilis/produksi.
  - **develop:** Tempat integrasi fitur-fitur baru sebelum akhirnya digabung ke main/master.
- **Branch per Fitur:** Setiap anggota tim membuat branch baru dari `develop` untuk fitur yang sedang dikerjakan, lalu merge kembali ke `develop` setelah selesai dan review.

**2. Contoh Alur Kerja Kolaborasi:**

1. **Buat branch baru untuk fitur:**

```bash
git checkout develop
git pull
git checkout -b feature/nama-fitur
```

2. **Kerjakan fitur di branch tersebut, commit perubahan:**

```bash
git add .
git commit -m "Deskripsi perubahan"
```

3. **Push branch ke remote:**

```bash
git push origin feature/nama-fitur
```

4. **Merge ke develop (setelah review, misal via Pull Request di GitHub):**

- Ajukan Pull Request dari `feature/nama-fitur` ke `develop`.
- Setelah review dan tidak ada konflik, merge dilakukan oleh reviewer atau lead.

**3. Penamaan Branch:**

- Gunakan konvensi yang jelas, misal:
  - `feature/nama-fitur`
  - `bugfix/nama-bug`
  - `hotfix/nama-hotfix`
  - `release/versi`

**4. Best Practices:**

- **Jaga branch utama (main/master) selalu stabil dan siap rilis**.
- **Lakukan merge secara rutin** dari branch develop ke main/master setelah fitur-fitur stabil dan teruji.
- **Hapus branch yang sudah di-merge** untuk menjaga repo tetap rapi.
- **Gunakan Pull Request** untuk code review sebelum merge ke branch utama.
- **Branch Protection Rules:** Di GitHub, gunakan aturan proteksi branch agar hanya perubahan yang sudah direview yang bisa masuk ke branch utama.

**5. Resolusi Konflik:**

- Jika terjadi konflik saat merge, Git akan menandai bagian yang bermasalah. Selesaikan secara manual, lalu lanjutkan merge dengan:

```bash
git add .
git commit
git merge --continue
```

**Ringkasan Workflow Kolaborasi:**

| Tahap                | Branch Asal     | Branch Tujuan      | Aksi                        |
|----------------------|-----------------|--------------------|-----------------------------|
| Membuat fitur        | develop         | feature/xxx        | git checkout -b             |
| Selesai fitur        | feature/xxx     | develop            | Pull Request & merge        |
| Rilis ke produksi    | develop         | main/master        | Pull Request & merge        |
| Hotfix produksi      | main/master     | hotfix/xxx         | git checkout -b, merge ke develop & main |

Dengan workflow ini, setiap anggota tim bisa bekerja paralel tanpa saling mengganggu, proses review berjalan transparan, dan branch utama tetap stabil. Jika ingin lebih detail tentang Gitflow atau workflow lain, kamu bisa eksplorasi dokumentasi resmi atau tutorial lanjutan
