# Spec — NIKAH! Rencana Nikah

## Fitur 1 — Perencana budget
- **SHALL-1:** Pengguna mengisi tanggal nikah, jumlah tamu, budget total, dan kota/tipe acara.
  WHEN pengguna mengubah tamu/budget/tanggal THEN total estimasi & status dihitung ulang seketika.
- **SHALL-2:** Setiap pos biaya punya 3 tier (Hemat/Standar/Mewah) dengan harga default dari data riset 2026, dan tiap pos bisa diedit manual (angka bebas) atau dinonaktifkan (0).
  WHEN tier diubah THEN harga pos berubah ke default tier itu; WHEN angka diedit manual THEN tier pos itu jadi "Custom".
- **SHALL-3:** Catering dihitung sebagai `tamu × harga per pax × 1,1` (cadangan porsi 10%).
  WHEN tamu berubah THEN catering berubah proporsional.
- **SHALL-4:** Dana cadangan 10% dari subtotal (toggle, default ON) dan inflasi vendor 6%/tahun pro-rata sampai tanggal nikah (toggle, default ON) diterapkan ke total dan ditampilkan sebagai baris terpisah dengan label asumsi.
- **SHALL-5:** Status budget ditampilkan: "Cukup" bila total ≤ budget (dengan sisa), "Mepet" bila total ≤ budget × 1,1, "Kurang" bila lebih; tiap status menampilkan selisih rupiah dan satu saran pangkas dari pos terbesar.
- **SHALL-6:** Tiga preset sekali ketuk: Intimate (100 tamu, Hemat), Standar (300 tamu), Grand (500 tamu, Mewah) — mengisi semua input sekaligus.
- **SHALL-7:** Breakdown per pos tampil sebagai bar horizontal proporsional + persentase, dan "biaya per tamu" tampil sebagai statistik.

## Fitur 2 — Rencana nabung
- **SHALL-8:** Pengguna mengisi tabungan sekarang; aplikasi menghitung bulan tersisa sampai tanggal nikah dan cicilan nabung per bulan = (target − tabungan) ÷ bulan tersisa.
  WHEN target ≤ tabungan THEN tampil "Tabunganmu sudah cukup" (bukan angka negatif).
  WHEN tanggal sudah lewat / bulan tersisa 0 THEN tampil pesan yang benar, bukan NaN/Infinity.
- **SHALL-9:** Rencana nabung menampilkan target hari-H (total estimasi + buffer + inflasi), tabungan sekarang, kekurangan, dan nominal per bulan — semuanya konsisten dengan Fitur 1.

## Fitur 3 — Hitung mundur + weton
- **SHALL-10:** Countdown live (hari/jam/menit/detik) ke tanggal nikah, berdetak tiap detik.
  WHEN tanggal sudah lewat THEN tampil "Sudah lewat X hari" + ucapan, bukan angka negatif.
- **SHALL-11:** Weton tanggal nikah ditampilkan: nama hari + pasaran (Legi/Pahing/Pon/Wage/Kliwon) + total neptu, dihitung deterministik dari anchor 1970-01-01 = Kamis Wage.
  WHEN tanggal diubah THEN weton ikut berubah. Neptu hari: Minggu 5, Senin 4, Selasa 3, Rabu 7, Kamis 8, Jumat 6, Sabtu 9. Neptu pasaran: Legi 5, Pahing 9, Pon 7, Wage 4, Kliwon 8.
- **SHALL-12:** Ada label yang jelas bahwa weton/neptu adalah tradisi Primbon Jawa, bukan jaminan.

## Fitur 4 — Checklist timeline
- **SHALL-13:** 24 tugas dalam 5 fase (12–9 bln, 6–3 bln, 1 bln, 1 minggu, Hari H), masing-masing bisa dicentang; progres total tampil sebagai persen + cincin progres.
  WHEN semua tugas selesai THEN tampil perayaan (confetti) sekali.
- **SHALL-14:** Semua state (input budget, tier, edit manual, tabungan, checklist) tersimpan di localStorage dan pulih saat halaman dibuka lagi.

## Fitur 5 — Tips hemat dinamis
- **SHALL-15:** Tiga tips ditampilkan berdasarkan 3 pos biaya terbesar saat ini (tiap pos punya tip spesifik); bila pos terbesar berubah, tips ikut berubah.

## Non-fungsional
- **SHALL-16:** Mobile-first (lebar app max 480px, bottom tab bar 4 tab: Rencana, Nabung, Checklist, Hari-H); semua kontrol bisa dipakai dengan sentuhan; tidak ada teks placeholder/lorem ipsum; tidak ada tombol mati.
- **SHALL-17:** Tidak ada error console; semua angka diformat Rupiah Indonesia; tanggal diformat Indonesia.
- **SHALL-18:** Copy Bahasa Indonesia natural; harga dilabeli "Estimasi 2026 — kisaran pasar, cek ke vendor".
