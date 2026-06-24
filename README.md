# Setup Spreadsheet untuk Data Penelitian Game Resonance Odyssey

## Tujuan
Sistem ini dibuat untuk mengumpulkan data hasil bermain siswa dari berbagai sekolah dalam penelitian edukasi musik Nusantara.

## Data yang Dikumpulkan
- Nama Siswa
- Nama Sekolah
- Karakter yang dipilih
- Hasil Game (Menang/Kalah)
- Nyawa tersisa saat selesai
- Total jawaban benar
- Total jawaban salah
- Waktu penyelesaian
- Detail jawaban per soal (format: "Kota: Benar/Salah | Kota: Benar/Salah | ...")

## Langkah Setup

### 1. Buat Google Form
1. Buka [Google Forms](https://forms.google.com)
2. Buat form baru dengan pertanyaan berikut:
   - **Nama Siswa** (Jawaban pendek)
   - **Nama Sekolah** (Jawaban pendek)
   - **Karakter** (Jawaban pendek)
   - **Hasil Game** (Pilihan: Menang/Kalah)
   - **Nyawa Tersisa** (Jawaban pendek - angka)
   - **Total Benar** (Jawaban pendek - angka)
   - **Total Salah** (Jawaban pendek - angka)
   - **Waktu Selesai** (Jawaban pendek - tanggal/waktu)
   - **Detail Jawaban** (Paragraf - untuk data lengkap per soal)

### 2. Dapatkan Form ID dan Entry IDs
1. Setelah membuat form, klik "Kirim" dan salin URL form
2. URL akan terlihat seperti: `https://docs.google.com/forms/d/e/FORM_ID/viewform`
3. Ganti `YOUR_FORM_ID` di kode dengan `FORM_ID` tersebut

### 3. Dapatkan Entry IDs
1. Buka form di browser
2. Klik kanan pada halaman dan pilih "Inspect Element"
3. Cari elemen `<input>` untuk setiap pertanyaan
4. Cari atribut `name` yang dimulai dengan `entry.`
5. Catat entry IDs untuk setiap pertanyaan

### 4. Update Kode
Buka `index.html` dan cari fungsi `sendGameDataToSpreadsheet`, lalu update:
```javascript
const formUrl = 'https://docs.google.com/forms/d/e/1FAIpQLScqZ0E6JF0yOCgyU9CdywAkMdGo-cRWtDjYaM8eJa3ZPbBjig/formResponse';

formData.append('entry.595722973', state.playerName); // Nama Siswa
formData.append('entry.725280792', state.schoolName); // Nama Sekolah
formData.append('entry.96563292', state.charId); // Karakter
formData.append('entry.1117235510', win ? 'Menang' : 'Kalah'); // Hasil Game
formData.append('entry.450530510', state.lives); // Nyawa Tersisa
formData.append('entry.1655330258', state.answers.filter(a => a.correct).length); // Total Benar
formData.append('entry.1984621075', state.answers.filter(a => !a.correct).length); // Total Salah
formData.append('entry.439573770', new Date().toLocaleString('id-ID')); // Waktu Selesai
formData.append('entry.674416243', answersDetail); // Detail Jawaban
```

### 5. Test Sistem
1. Jalankan game di browser
2. Isi nama siswa dan nama sekolah
3. Mainkan sampai selesai
4. Periksa spreadsheet yang terhubung dengan form
5. Data harus muncul otomatis

## Analisis Data
Dengan data ini, Anda dapat menganalisis:
- Tingkat pemahaman siswa per topik musik daerah
- Performa siswa berdasarkan sekolah
- Pola kesalahan yang umum
- Efektivitas game sebagai media pembelajaran

## Keamanan Data
- Pastikan Google Form di-set private
- Hanya share link form kepada sekolah yang berpartisipasi
- Data tersimpan secara otomatis di Google Sheets untuk analisis
