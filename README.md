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

---

Untuk melakukan merge branch `feature/feature1` ke branch `develop`, kamu bisa ikuti langkah-langkah berikut:

1. **Pindah ke branch develop:**
   ```bash
   git checkout develop
   ```
2. **Update branch develop agar sinkron dengan remote (opsional tapi disarankan):**
   ```bash
   git pull origin develop
   ```
3. **Lakukan merge branch feature/feature1 ke develop:**
   ```bash
   git merge feature/feature1
   ```
   - Jika tidak ada konflik, Git akan menggabungkan perubahan dan membuat merge commit secara otomatis.
   - Jika ada konflik, Git akan memberitahu file mana yang perlu kamu selesaikan secara manual.

4. **Setelah merge selesai dan commit sudah dibuat, kamu bisa menghapus branch feature/feature1 jika sudah tidak diperlukan:**
   ```bash
   git branch -d feature/feature1
   ```

### Opsi tambahan untuk merge

- Jika kamu ingin membuat merge commit walaupun Git bisa melakukan fast-forward merge (agar riwayat merge lebih jelas), gunakan:
  ```bash
  git merge --no-ff feature/feature1
  ```
- Jika kamu ingin riwayat commit jadi lebih rapi dengan menggabungkan semua commit di feature branch menjadi satu commit sebelum merge, kamu bisa melakukan squash merge secara manual:
  ```bash
  git checkout feature/feature1
  git rebase -i develop
  git checkout develop
  git merge --squash feature/feature1
  git commit -m "Gabungkan fitur feature1 ke develop"
  ```

### Alternatif: Merge via Pull Request di GitHub

Kalau kamu menggunakan GitHub, biasanya workflow kolaborasi yang baik adalah:

- Push branch `feature/feature1` ke remote.
- Buat **Pull Request** dari `feature/feature1` ke `develop`.
- Lakukan review dan diskusi kode.
- Setelah disetujui, merge PR melalui antarmuka GitHub dengan opsi merge yang tersedia (merge commit, squash and merge, atau rebase and merge).

Dengan langkah-langkah tersebut, kamu bisa menggabungkan fitur yang sudah selesai ke branch develop dengan aman dan terstruktur[1][2][3][4].

[1] https://liupurnomo.com/git-flow-untuk-pemula-yang-mau-tampil-pro/
[2] https://www.atlassian.com/git/tutorials/using-branches/git-merge
[3] https://www.hostinger.com/id/tutorial/perintah-git-dasar
[4] https://www.dicoding.com/blog/cara-berkolaborasi-di-repositori-github/
[5] https://dev.to/yudhasdev/tutorial-github-3-bagaimana-cara-menggunakan-branch-dan-merge-di-github-3nj1
[6] https://www.hostinger.com/id/tutorial/git-branch
[7] https://dev.to/mandaputtra/git-workflow-mudah-kok-1d5g
[8] https://soaltekno.lokercepat.id/bagaimana-cara-menyelesaikan-konflik-merge-di-git/