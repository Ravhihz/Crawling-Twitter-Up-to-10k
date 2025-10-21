🚀 Crawling & Auto-Resume Pipeline (Colab + Google Drive)

ID & EN disediakan dalam satu berkas README agar mudah dipakai komunitas global.

🇮🇩 Ringkasan (Bahasa Indonesia)

Pipeline ini dirancang untuk crawling data yang tahan putus dan ramah Colab. Proyek sudah:

✅ Pakai auth token pengguna masing-masing (aman & fleksibel).

✅ Tetap berjalan walaupun layar laptop mati / sleep (headless friendly).

✅ Auto-save state dan auto-resume saat runtime baru dimulai.

✅ Auto-merge hasil crawling setelah selesai (gabung CSV/log).

✅ Terintegrasi dengan Google Drive (penyimpanan hasil & state).

Jika ada pertanyaan: ravhi.satria@gmail.com
.

✨ Fitur Utama

Auto-save & Auto-resume: Menyimpan checkpoint/state berkala (mis. state.json) dan melanjutkan pekerjaan tanpa mengulang.

Headless-safe: Proses tetap aman walau tab tidak aktif/laptop sleep.

Auto-merge artifact: Menggabungkan hasil (mis. CSV) menjadi satu berkas final.

Integrasi Google Drive: Output dan state tersimpan ke Drive agar aman saat runtime reset.

Auth token per pengguna: Gunakan token kamu sendiri (mis. API key / session token) tanpa mengubah kode inti.

📦 Prasyarat

Akun Google & akses Google Colab.

Google Drive aktif.

Auth token dari layanan yang kamu crawling (letakkan aman – lihat bagian Keamanan).

🔐 Konfigurasi Token (wajib)

Simpan token sebagai variabel lingkungan (contoh Colab):

import os
os.environ["MY_AUTH_TOKEN"] = "isi-token-kamu-di-sini"  # JANGAN commit ke Git!


Jangan menaruh token di kode sumber atau README. Pakai Environment Variables/Colab secrets.

☁️ Hubungkan Google Drive (Colab)
from google.colab import drive
drive.mount('/content/drive')
# Set folder kerja, mis.:
WORKDIR = "/content/drive/MyDrive/proyek-crawling"

▶️ Menjalankan Pipeline (Contoh)
# 1) Set token & path output
import os, pathlib
os.environ["MY_AUTH_TOKEN"] = "token-kamu"
OUTPUT_DIR = pathlib.Path(WORKDIR) / "outputs"
OUTPUT_DIR.mkdir(parents=True, exist_ok=True)

# 2) Jalankan crawler (contoh fungsi)
from my_pipeline import run_crawl  # contoh modul
run_crawl(
  token=os.environ["MY_AUTH_TOKEN"],
  out_dir=str(OUTPUT_DIR),
  auto_resume=True,
  save_every=500   # simpan state tiap 500 item
)

🔄 Auto-Resume Bekerja Bagaimana?

State (mis. state.json) disimpan berkala (jumlah baris, daftar window/batch yang sudah selesai, timestamp).

Saat start ulang, kode akan:

Mendeteksi state.

Melewati bagian yang sudah selesai.

Melanjutkan dari checkpoint terakhir.

🔗 Auto-Merge Hasil

Setelah semua batch selesai, pipeline otomatis menggabungkan mis. *.csv menjadi:

outputs/
 ├─ raw/...
 ├─ merged_all.csv   ← hasil akhir
 └─ logs/...

🧯 Troubleshooting

Notebook putus/Colab reset → normal: cukup run ulang; auto-resume akan lanjutkan.

Token invalid/expired → perbarui MY_AUTH_TOKEN.

Google Drive penuh → kosongkan ruang atau ganti lokasi output.

Duplikasi baris (akibat beberapa batch) → gunakan opsi dedup (jika disediakan) atau jalankan pembersihan pasca-merge.

🔒 Keamanan

Simpan token di env var / Colab secrets, jangan commit.

Jika repo publik, tambahkan ke .gitignore:

state.json
*.env
outputs/
drive/

🤝 Kontribusi

PR & issue dipersilakan (bug, dokumentasi, feature request).

📄 Lisensi

Tentukan lisensi (mis. MIT/Apache-2.0). Buat file LICENSE.

📬 Kontak

ravhi.satria@gmail.com

🇬🇧 Overview (English)

A fault-tolerant crawling pipeline built for Google Colab. It already:

✅ Uses per-user auth tokens.

✅ Keeps running headlessly even if your laptop sleeps.

✅ Auto-saves state and auto-resumes on a fresh runtime.

✅ Auto-merges crawl outputs at the end.

✅ Is integrated with Google Drive for persistent storage.

Questions? ravhi.satria@gmail.com
.

✨ Key Features

Auto-save & Auto-resume: Checkpointing to state.json (or similar), resuming without rework.

Headless-safe: Safe to run when the tab is inactive / device sleeps.

Auto-merge artifacts: Collate multi-batch outputs (e.g., CSV) into a single file.

Google Drive integration: Keep outputs/state across runtime resets.

Per-user auth token: Bring your own token without code changes.

📦 Requirements

Google account & Google Colab access.

Google Drive enabled.

A valid auth token for the target service (see Security).

🔐 Token Setup (required)

Use environment variables (example in Colab):

import os
os.environ["MY_AUTH_TOKEN"] = "put-your-token-here"  # NEVER commit to Git!

☁️ Mount Google Drive (Colab)
from google.colab import drive
drive.mount('/content/drive')
WORKDIR = "/content/drive/MyDrive/crawling-project"

▶️ Run the Pipeline (Example)
# 1) Configure token & output path
import os, pathlib
os.environ["MY_AUTH_TOKEN"] = "your-token"
OUTPUT_DIR = pathlib.Path(WORKDIR) / "outputs"
OUTPUT_DIR.mkdir(parents=True, exist_ok=True)

# 2) Launch crawler (example)
from my_pipeline import run_crawl  # example module
run_crawl(
  token=os.environ["MY_AUTH_TOKEN"],
  out_dir=str(OUTPUT_DIR),
  auto_resume=True,
  save_every=500
)

🔄 How Auto-Resume Works

Periodically writes a state file (e.g., processed batches, total rows, timestamps).

On restart:

Detects existing state,

Skips completed work,

Continues from the latest checkpoint.

🔗 Auto-Merge Output

After all batches finish, the pipeline merges artifacts (e.g., *.csv) into:

outputs/
 ├─ raw/...
 ├─ merged_all.csv   ← final result
 └─ logs/...

🧯 Troubleshooting

Runtime reset / disconnect → just rerun; auto-resume will continue.

Invalid/expired token → refresh MY_AUTH_TOKEN.

Drive quota exceeded → free space or switch output location.

Duplicate rows (multi-batch) → enable dedup option or run a cleanup script.

🔒 Security

Keep tokens in env vars / Colab secrets; never commit them.

For public repos, add to .gitignore:

state.json
*.env
outputs/
drive/

🤝 Contributing

PRs and issues are welcome.

📄 License

Choose a license (e.g., MIT/Apache-2.0) and add a LICENSE file.

📬 Contact

ravhi.satria@gmail.com
