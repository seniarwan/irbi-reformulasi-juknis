# Petunjuk Teknis Reformulasi IRBI Nasional — Situs Quarto

Situs dokumentasi multi-halaman untuk "Petunjuk Teknis Reformulasi Indeks Risiko Bencana (IRBI) Nasional", dibangun dengan [Quarto](https://quarto.org). Versi dashboard 0.8 berisi delapan bab, delapan lampiran operasional, enam ilustrasi konsep/alur, dan register berisi 18 isu metodologis: 12 terbuka dan 6 selesai. Situs ini merupakan ruang kerja penyusunan juknis dan belum menyajikan dashboard hasil IRBI nasional per wilayah.

## Struktur proyek

```
_quarto.yml              # konfigurasi situs (sidebar, tema, format)
index.qmd                # halaman depan dengan kartu ringkasan
bab-1.qmd … bab-8.qmd    # delapan bab juknis
lampiran-a.qmd … lampiran-h.qmd
register-isu.qmd        # register keputusan metodologis
data/isu_terbuka.csv    # sumber register yang dapat diunduh
assets/figures/         # enam ilustrasi konsep dan alur
styles.scss / styles.css # tema, kartu, metrik, dan register isu
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

Dokumen ini berstatus **draf kerja, belum normatif**. Enam butir telah diselesaikan. Selain koreksi formula, kalibrasi, dan daftar 11 bahaya, M-05 menetapkan bahwa HM dan VM ditransformasi terlebih dahulu sebelum membentuk `RP=sqrt(HM*VM)`. M-06 menetapkan domain IKD 0,20-1,00, sehingga C minimum adalah 1/6 atau sekitar 0,17 dan `C=0` tidak mungkin pada input sah. Register masih memuat 12 isu terbuka, termasuk 5 isu kritis mengenai klasifikasi, kedudukan RA, identitas skenario, satuan input, dan penggabungan data wilayah.

Contoh Aceh Selatan menggunakan urutan normatif M-05. Komponen input tetap direkonsiliasi dengan workbook, sedangkan perbedaan kecil pada RP, RA, dan RR terhadap keluaran workbook lama dicatat sebagai dampak perubahan urutan transformasi.
