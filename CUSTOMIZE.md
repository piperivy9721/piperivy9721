# 📘 Panduan Menyesuaikan Profil

README di repo ini otomatis tampil di <https://github.com/piperivy9721>.
Semua yang perlu diganti ada di `README.md` — bagian yang harus diisi ditandai `<...>`,
dan bagian opsional ditandai komentar `OPSIONAL`.

## 1. Yang wajib diganti

| Lokasi di README | Isi dengan |
| --- | --- |
| Blok `yaml` di **About Me** | nama, peran, lokasi, fokus, hal yang sedang dipelajari |
| Quote di bawah blok About Me | motto / kalimat favoritmu |
| Banner atas | `text=`, `desc=`, dan `fontColor=` di URL `capsule-render` |
| Tagline berjalan | bagian `&lines=` di URL `readme-typing-svg` (pisahkan tiap baris dengan `;`) |
| Badge **Tech Stack** | hapus baris yang tidak kamu pakai |

Semua URL memakai `?username=piperivy9721` / `user=piperivy9721`. Kalau repo ini
dipakai untuk akun lain, ganti string tersebut.

## 2. Bagian opsional

- **Sosial media & email** — ada di dalam komentar di bagian *Let's Connect*.
  Ganti `LINK-KAMU` / `EMAIL-KAMU`, lalu hapus pembungkus `<!-- -->`.
- **Trophy & Activity Graph** — di dalam komentar di bagian *GitHub Stats*.
  Dua layanan itu kadang membalas error 402 (rate limit bersama), jadi
  sebaiknya diaktifkan hanya kalau sudah normal.
- **Animasi snake** — gambar dihasilkan oleh workflow GitHub Actions.
  Buat file `.github/workflows/snake.yml` **lewat web UI GitHub**
  (Add file → Create new file), lalu tempel isi berikut:

  ```yaml
  name: 🐍 Generate Snake Animation

  on:
    schedule:
      - cron: "0 0 * * *" # setiap hari 00:00 UTC = 07:00 WIB
    workflow_dispatch: # bisa dijalankan manual dari tab Actions
    push:
      branches: [main]

  jobs:
    generate:
      runs-on: ubuntu-latest
      permissions:
        contents: write
      steps:
        - name: Generate snake SVG
          uses: Platane/snk/svg-only@v3
          with:
            github_user_name: piperivy9721
            outputs: |
              dist/github-snake.svg
              dist/github-snake-dark.svg?palette=github-dark

        - name: Publish ke branch output
          uses: crazy-max/ghaction-github-pages@v4
          with:
            target_branch: output
            build_dir: dist
          env:
            GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
  ```

  Setelah commit, buka tab **Actions → 🐍 Generate Snake Animation → Run workflow**.
  Kalau branch `output` sudah berisi `github-snake.svg`, hapus pembungkus komentar
  pada blok snake di `README.md`.

## 3. Tips tampilan

- Gaya badge dijaga konsisten: `style=flat-square` untuk tech stack,
  `style=for-the-badge` untuk tombol sosial.
- Setiap kartu statistik memakai `<picture>` + `prefers-color-scheme`, jadi
  otomatis ikut mode terang/gelap GitHub — jangan hapus tag `<picture>`-nya.
- Semakin ringkas semakin rapi: 6–8 badge per kategori sudah cukup.

## 4. Cara publish

Default branch repo ini (`main`) adalah yang dibaca GitHub untuk halaman profil.
Setelah perubahan di-merge ke `main`, halaman profil langsung ter-update
(mungkin perlu hard refresh). Tema di palet ini: ungu `#8B5CF6` → cyan `#22D3EE`.

> **Catatan:** saat README ini dibuat, repo masih kosong sehingga GitHub memakai
> branch `cline/e9hqr43a` sebagai default branch. Branch `main` sudah dibuat dengan
> isi yang sama. Ubah default branch ke `main` lewat
> **Settings → General → Default branch**, atau dari terminal:
>
> ```bash
> gh repo edit --default-branch main
> ```
>
> Selama salah satu branch tersebut tetap jadi default, halaman profil tetap tampil normal.
