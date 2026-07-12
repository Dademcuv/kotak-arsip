# Kotak Arsip — Setup dari HP

Web ini 1 file (`index.html`) berisi form upload + galeri foto/video yang tersimpan di **Supabase Storage** milikmu sendiri. Semua bisa dikerjakan dari HP pakai Acode/Spck Editor.

## 1. Buat project Supabase (gratis)

1. Buka https://supabase.com lewat browser HP, daftar/login.
2. Klik **New Project** → kasih nama bebas → pilih region terdekat (Singapore) → simpan password database (nggak akan dipakai di web ini, tapi wajib diisi).
3. Tunggu ± 2 menit sampai project siap.

## 2. Buat storage bucket

1. Di sidebar project, buka **Storage**.
2. Klik **New bucket** → nama: `media` → aktifkan **Public bucket** (supaya foto bisa tampil lewat URL langsung).
3. Setelah bucket dibuat, buka tab **Policies** pada bucket `media`, klik **New Policy** → pilih template **"Enable read access for all users"** dan **"Enable insert/delete for authenticated users"** kalau mau lebih aman (butuh login), atau untuk versi paling simpel (personal use, nggak ada login) pakai template **"Enable all access for all users"** — cukup untuk dipakai sendiri, tapi diingat ini artinya siapa saja yang tahu URL bucket bisa upload/hapus. Untuk yang lebih aman, tambahkan Supabase Auth di iterasi berikutnya.

## 3. Ambil kredensial API

1. Di sidebar, buka **Project Settings → API**.
2. Salin **Project URL** dan **anon public key**.

## 4. Isi kredensial ke index.html

Buka `index.html` di Acode/Spck Editor, cari bagian ini di paling bawah file dan isi:

```js
const SUPABASE_URL = "https://xxxxxxxxxxxx.supabase.co";
const SUPABASE_ANON_KEY = "isi-anon-key-supabase-kamu-di-sini";
const BUCKET_NAME = "media";
```

Ganti dengan URL dan anon key dari langkah 3. Nama bucket biarkan `media` kalau ikut langkah 2, atau sesuaikan.

## 5. Upload ke GitHub lewat HP

1. Install app **GitHub** (opsional, buat cek) atau langsung lewat browser mobile ke https://github.com/new → buat repo baru, misal `kotak-arsip`.
2. Cara paling gampang dari HP: buka repo di browser → **Add file → Upload files** → upload `index.html` (dan `README.md` kalau mau).
3. Kalau pakai Acode/Spck, keduanya juga punya fitur Git client bawaan/plugin — bisa `git init`, `git remote add`, `git push` langsung dari app kalau sudah nyaman pakai Termux atau plugin Git di editor tersebut.

## 6. Aktifkan GitHub Pages

1. Di repo GitHub, buka **Settings → Pages**.
2. Source: pilih branch `main`, folder `/ (root)` → **Save**.
3. Tunggu ± 1 menit, web akan aktif di `https://<username>.github.io/kotak-arsip/`.

Alternatif: connect repo yang sama ke **Vercel** atau **Netlify** (login pakai akun GitHub, pilih repo, deploy) — keduanya juga bisa dilakukan dari browser HP tanpa command line.

## Catatan keamanan

- Karena `anon key` ditulis langsung di file HTML (client-side), key ini memang didesain aman untuk publik dipakai bersama Row Level Security/Policy Supabase — tapi tetap atur policy bucket sesuai kebutuhan (lihat langkah 2).
- Kalau nanti mau web ini private (cuma kamu yang bisa akses), tambahkan Supabase Auth (login email/Google) dan ubah policy bucket jadi "authenticated users only" — bisa dibantu iterasi berikutnya kalau dibutuhkan.

## Yang bisa dikembangkan lagi

- Tambah login (Supabase Auth) supaya cuma kamu yang bisa upload/lihat.
- Tambah folder/album.
- Kompresi otomatis sebelum upload video besar.
