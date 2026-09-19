# Petunjuk Teknis Reformulasi IRBI Nasional — Situs Quarto

Situs dokumentasi multi-halaman untuk "Petunjuk Teknis Reformulasi Indeks Risiko Bencana (IRBI) Nasional", dibangun dengan [Quarto](https://quarto.org). Berisi 8 BAB metodologi perhitungan dan 4 Lampiran (parameter, bobot, contoh perhitungan lengkap, checklist mutu). Tidak memuat visualisasi data nasional per-provinsi — situs ini murni dokumentasi metodologi juknis.

## Struktur proyek

```
_quarto.yml              # konfigurasi situs (sidebar, tema, format)
index.qmd                # halaman depan dengan kartu ringkasan
bab-1.qmd … bab-8.qmd    # delapan bab juknis
lampiran-a.qmd … lampiran-d.qmd
styles.scss / styles.css # tema dan gaya kartu ringkasan
favicon.svg
.github/workflows/publish.yml  # auto-publish ke GitHub Pages
```

## Menjalankan secara lokal

Perlu [Quarto CLI](https://quarto.org/docs/get-started/) versi 1.6 atau lebih baru terpasang.

```bash
quarto preview
```

Ini akan membuka pratinjau situs di browser dan memuat ulang otomatis saat file `.qmd` diubah.

Untuk merender situs statis ke folder `docs/` (tanpa preview):

```bash
quarto render
```

## Publikasi ke GitHub Pages

### Opsi A — Otomatis lewat GitHub Actions (direkomendasikan)

Repo ini sudah menyertakan `.github/workflows/publish.yml`, yang akan merender dan mempublikasikan situs ke branch `gh-pages` setiap kali ada push ke `main`.

1. Buat repository baru di GitHub, lalu push proyek ini:

   ```bash
   git init
   git add .
   git commit -m "Inisialisasi situs juknis IRBI reformulasi"
   git branch -M main
   git remote add origin https://github.com/<username>/<nama-repo>.git
   git push -u origin main
   ```

2. Di GitHub, buka **Settings → Pages**, lalu pada **Build and deployment → Source** pilih **Deploy from a branch**, dan set branch ke `gh-pages` / folder `/ (root)`. (Branch `gh-pages` akan otomatis dibuat oleh workflow setelah push pertama ke `main` selesai diproses — cek tab **Actions** untuk memastikan workflow berjalan sukses terlebih dahulu.)

3. Setelah workflow selesai (biasanya 1–2 menit), situs akan tersedia di:

   ```
   https://<username>.github.io/<nama-repo>/
   ```

4. Setiap push berikutnya ke `main` akan otomatis merender ulang dan memperbarui situs.

### Opsi B — Manual lewat `quarto publish`

Alternatif tanpa GitHub Actions, langsung dari komputer lokal:

```bash
quarto publish gh-pages
```

Perintah ini akan merender situs dan mem-push hasilnya ke branch `gh-pages` di repo yang sudah di-*remote*-kan, lalu menampilkan URL situs yang dihasilkan.

## Catatan isi

Dokumen ini mencantumkan dua isu terbuka yang belum final secara resmi (lihat kotak peringatan di `index.qmd`, Bab III.3.3, Bab VI, dan Lampiran C):

1. Satuan Kerugian Fisik/Ekonomi pada data proyeksi 2025 tampak tidak konsisten dengan ambang Lampiran A.
2. Nilai $x_{max}$ untuk penyetaraan skala kelas risiko tinggi (Bab VII / Lampiran C Langkah 8) belum dinyatakan angkanya secara resmi oleh BNPB.

Perbarui bagian-bagian ini bila BNPB sudah menerbitkan angka/keputusan final.
