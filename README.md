# Praktikum 7: PHP Dasar (Form Data Diri)

> **Nama:** Anggriani Hermawan 
> **Mata Kuliah:** Pemrograman Web  
> **NIM:** 312410175 
> **Dosen:** Agung Nugroho, S.Kom., M.Kom

---

## Tujuan Praktikum

1. Mahasiswa mampu memahami dasar **server-side scripting (PHP)**.  
2. Mahasiswa mampu memahami **variabel, tipe data, kondisi, dan perulangan** dalam PHP.  
3. Mahasiswa mampu **membuat form input data** dan memprosesnya menggunakan PHP.  
4. Mahasiswa mampu **menghitung data dinamis** (seperti umur & gaji) dengan tampilan yang menarik.

---

## Membuat Struktur Folder

Lokasi project:
Di dalamnya buat dua file:
- `index.php` → untuk form input data diri  
- `proses.php` → untuk menampilkan hasil perhitungan
<img width="218" height="53" alt="Cuplikan layar 2025-11-10 134143" src="https://github.com/user-attachments/assets/c3c7d5ab-e223-4bdc-b673-441529bddbfc" />

## Langkah 1: Membuat Struktur Dasar HTML
File: index.html
Tujuan: Membuat kerangka awal halaman web untuk form data diri.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Form Data Diri - Pink Style</title>
</head>
<body>
    <div class="container">
        <h2> Form Data Diri dan Penghitungan Gaji </h2>

        <form method="post" action="proses.php">
            <!-- Input akan ditambahkan di langkah berikut -->
        </form>
    </div>
</body>
</html>
```
Penjelasan:
- <!DOCTYPE html> → menandakan dokumen ini HTML5.
- <html lang="en"> → mendefinisikan bahasa halaman.
- <head> → berisi metadata, judul, dan nanti CSS.
- <body> → berisi konten utama yang akan terlihat di browser.
- <div class="container"> → wadah utama form agar tampil rapi di tengah.
<img width="1920" height="1080" alt="Cuplikan layar 2025-11-10 134912" src="https://github.com/user-attachments/assets/14cd68fb-8d4c-4dc0-924c-38494345f123" />

## Langkah 2: Menambahkan CSS (Tampilan Warna Soft Pink)
Tambahkan kode CSS di dalam tag <style> pada bagian <head>.
```
<style>
    /* CSS untuk tampilan soft pink */
    body {
        font-family: Arial, sans-serif;
        background-color: #fce4ec; /* Soft Pink / Rose Pink Light */
        color: #333;
        margin: 0;
        padding: 20px;
    }
    .container {
        max-width: 500px;
        margin: 50px auto;
        padding: 30px;
        background-color: #fff; /* Latar belakang konten putih */
        border-radius: 15px;
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }
    h2 {
        color: #e91e63; /* Deep Pink */
        text-align: center;
        border-bottom: 2px solid #f8bbd0; /* Garis bawah pink muda */
        padding-bottom: 10px;
        margin-bottom: 20px;
    }
</style>
```
Penjelasan:
- background-color: #fce4ec; → warna pink lembut untuk halaman.
- .container → area utama form diberi background putih & bayangan halus.
- h2 → judul dengan warna pink tua dan garis bawah lembut.
<img width="1920" height="1080" alt="Cuplikan layar 2025-11-10 131625" src="https://github.com/user-attachments/assets/7bfb9d3c-f82f-4203-82e4-1865441948a2" />

## Langkah 3: Mendesain Input dan Tombol
Masih di dalam tag <style>, tambahkan bagian berikut agar form-nya rapi dan elegan:
```
input[type="text"], input[type="date"], select {
    width: 100%;
    padding: 10px;
    margin-bottom: 15px;
    border: 1px solid #f8bbd0; /* Border pink muda */
    border-radius: 5px;
    box-sizing: border-box;
}
input[type="submit"] {
    background-color: #e91e63; /* Tombol Deep Pink */
    color: white;
    padding: 12px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    transition: background-color 0.3s ease;
}
input[type="submit"]:hover {
    background-color: #c2185b; /* Warna pink tua saat hover */
}
label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
    color: #d81b60; /* Label Pink */
}
```
Penjelasan:
- Semua input (text, date, select) dibuat full-width agar simetris.
- input[type=submit] → tombol pink lembut, berubah jadi lebih tua saat hover.
- label → warna pink medium untuk teks di atas setiap input.

## Langkah 4: Membuat Input Nama Lengkap
Tambahkan input pertama di dalam <form>.
```
<label for="nama">Nama Lengkap:</label>
<input type="text" id="nama" name="nama" required>
```
Penjelasan:
- for="nama" dan id="nama" menghubungkan label dengan input.
- required memastikan kolom harus diisi sebelum dikirim.
<img width="1920" height="1080" alt="Cuplikan layar 2025-11-10 131703" src="https://github.com/user-attachments/assets/8aaf5b0c-44d7-4211-b0f6-b6fa38ff85f5" />

## Langkah 5: Membuat Input Tanggal Lahir
Tambahkan baris ini setelah input nama:
```
<label for="tgl_lahir">Tanggal Lahir:</label>
<input type="date" id="tgl_lahir" name="tgl_lahir" required>
```
Penjelasan:
- type="date" akan memunculkan kalender untuk memilih tanggal.
- Digunakan untuk menghitung umur nantinya di file proses.php.
<img width="1920" height="1080" alt="Cuplikan layar 2025-11-10 131733" src="https://github.com/user-attachments/assets/f710fad8-f905-42e8-843b-389214aa1b13" />

## Langkah 6: Membuat Dropdown Pekerjaan
Tambahkan setelah input tanggal lahir:
```
<label for="pekerjaan">Pilih Pekerjaan:</label>
<select id="pekerjaan" name="pekerjaan" required>
    <option value="">-- Pilih Pekerjaan --</option>
    <option value="programmer">Programmer</option>
    <option value="designer">Desainer Grafis</option>
    <option value="manager">Manajer Proyek</option>
    <option value="marketing">Staf Marketing</option>
</select>
```
Penjelasan:
- Dropdown select berisi 4 opsi pekerjaan.
- Nilai (value) dikirim ke file proses untuk menentukan gaji nanti.
- Opsi pertama kosong agar pengguna wajib memilih.
<img width="1920" height="1080" alt="Cuplikan layar 2025-11-10 131801" src="https://github.com/user-attachments/assets/d1681364-3416-4d73-bde8-82101ec00268" />
<img width="227" height="128" alt="Cuplikan layar 2025-11-10 131823" src="https://github.com/user-attachments/assets/52425bf6-4a3a-4c94-92e5-f8f1b8f3683a" />

## Langkah 7: Membuat Tombol Kirim
Tambahkan di akhir <form>:
```
<input type="submit" value="Kirim Data">
```
Penjelasan:
- Tombol berwarna deep pink untuk mengirimkan data form.
- Saat ditekan, data dikirim ke file proses.php menggunakan metode POST.
<img width="1920" height="1080" alt="Cuplikan layar 2025-11-10 131852" src="https://github.com/user-attachments/assets/d9dd1f05-9969-4227-bb5e-be2817482e2b" />

## Langkah 8 Tampilan Akhir Halaman (Sebelum Form di Isi)
```
<?php
} else {
?>
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Akses Ditolak!</title>
    <style>
        body {
            background-color: #fdeef3;
            font-family: "Poppins", Arial, sans-serif;
            text-align: center;
            padding-top: 120px;
            color: #d81b60;
        }
        .warning-box {
            background-color: #fff;
            display: inline-block;
            padding: 40px 50px;
            border-radius: 20px;
            box-shadow: 0 6px 15px rgba(0,0,0,0.1);
            max-width: 480px;
            line-height: 1.6;
        }
        h2 {
            color: #d81b60;
            font-size: 26px;
            margin-bottom: 10px;
        }
        p {
            color: #c2185b;
            font-size: 15px;
            margin-bottom: 25px;
        }
        a {
            display: inline-block;
            background-color: #f8bbd0;
            color: #d81b60;
            font-weight: bold;
            padding: 10px 20px;
            border-radius: 8px;
            text-decoration: none;
            transition: all 0.3s ease;
        }
        a:hover {
            background-color: #f48fb1;
        }
        .icon {
            font-size: 40px;
        }
    </style>
</head>
<body>
    <div class="warning-box">
        <div class="icon"></div>
        <h2>Akses Ditolak!</h2>
        <p>Silakan isi form terlebih dahulu sebelum membuka halaman ini.</p>
        <a href="index.php"> Kembali ke Form Input</a>
    </div>
</body>
</html>
<?php
exit;
}
?>
```
Penjelasan:
- body	Warna dasar pink lembut #fdeef3 dan teks rata tengah
- .warning-box	Kotak putih dengan bayangan lembut di tengah halaman
- h2	Judul “Akses Ditolak!” berwarna pink tua
- p	Pesan keterangan agar user kembali ke form
- a	Tombol pink muda yang bisa diklik untuk kembali ke index.php
<img width="1920" height="1080" alt="Cuplikan layar 2025-11-10 133727" src="https://github.com/user-attachments/assets/f21faca6-c99e-468c-aa9b-6ee536b3dfc6" />

## Langkah 9 Mengisi Form
<img width="1920" height="1080" alt="Cuplikan layar 2025-11-10 132024" src="https://github.com/user-attachments/assets/74d10cfa-5fbe-42c7-8510-aa7cd75eca1c" />

## Langkah 10 Tampilan Akhir Setelah di Isi
```
<?php
// ===============================================
// FILE : proses.php
// FUNGSI : Menerima data dari index.php,
// menghitung umur dan menampilkan hasil
// dengan tampilan pink lembut dan aman.
// ===============================================

// Cek apakah data dikirim melalui POST dan valid
if ($_SERVER["REQUEST_METHOD"] == "POST" && isset($_POST['nama']) && isset($_POST['tgl_lahir']) && isset($_POST['pekerjaan'])) {
    
    // 1️ Ambil data dari form
    $nama = $_POST['nama'];
    $tgl_lahir_str = $_POST['tgl_lahir'];
    $pekerjaan = $_POST['pekerjaan'];

    // 2️ Hitung umur berdasarkan tanggal lahir
    $tgl_lahir = new DateTime($tgl_lahir_str);
    $today = new DateTime('today');
    $umur = $today->diff($tgl_lahir)->y;

    // 3️ Tentukan gaji berdasarkan pekerjaan
    $gaji = 0;
    $nama_pekerjaan = "";

    switch ($pekerjaan) {
        case "programmer":
            $gaji = 8000000;
            $nama_pekerjaan = "Programmer";
            break;
        case "designer":
            $gaji = 5500000;
            $nama_pekerjaan = "Desainer Grafis";
            break;
        case "manager":
            $gaji = 12000000;
            $nama_pekerjaan = "Manajer Proyek";
            break;
        case "marketing":
            $gaji = 4000000;
            $nama_pekerjaan = "Staf Marketing";
            break;
        default:
            $gaji = 0;
            $nama_pekerjaan = "Pekerjaan Tidak Diketahui";
            break;
    }

    // Format gaji ke format Rupiah
    $gaji_formatted = "Rp " . number_format($gaji, 0, ',', '.');

} else {
    // =======================================================
    // Tampilan jika user membuka langsung proses.php tanpa form
    // =======================================================
    ?>
    <!DOCTYPE html>
    <html lang="id">
    <head>
        <meta charset="UTF-8">
        <title>Akses Ditolak!</title>
        <style>
            body {
                background-color: #fdeef3;
                font-family: "Poppins", Arial, sans-serif;
                text-align: center;
                padding-top: 120px;
                color: #d81b60;
            }
            .warning-box {
                background-color: #fff;
                display: inline-block;
                padding: 40px 50px;
                border-radius: 20px;
                box-shadow: 0 6px 15px rgba(0,0,0,0.1);
                max-width: 480px;
                line-height: 1.6;
                animation: fadeIn 0.7s ease;
            }
            h2 {
                color: #d81b60;
                font-size: 26px;
                margin-bottom: 10px;
            }
            p {
                color: #c2185b;
                font-size: 15px;
                margin-bottom: 25px;
            }
            a {
                display: inline-block;
                background-color: #f8bbd0;
                color: #d81b60;
                font-weight: bold;
                padding: 10px 20px;
                border-radius: 8px;
                text-decoration: none;
                transition: all 0.3s ease;
            }
            a:hover {
                background-color: #f48fb1;
            }
            .icon {
                font-size: 40px;
                margin-bottom: 10px;
            }
            @keyframes fadeIn {
                from { opacity: 0; transform: translateY(-10px); }
                to { opacity: 1; transform: translateY(0); }
            }
        </style>
    </head>
    <body>
        <div class="warning-box">
            <div class="icon"></div>
            <h2>Akses Ditolak!</h2>
            <p>Silakan isi form terlebih dahulu sebelum membuka halaman ini.</p>
            <a href="index.php"> Kembali ke Form Input</a>
        </div>
    </body>
    </html>
    <?php
    exit;
}
?>

<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Hasil Data Diri - Pink Style</title>
    <style>
        body {
            font-family: "Poppins", Arial, sans-serif;
            background-color: #fce4ec;
            color: #333;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 500px;
            margin: 50px auto;
            padding: 30px;
            background-color: #fff;
            border-radius: 15px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            animation: fadeIn 0.7s ease;
        }
        h2 {
            color: #e91e63;
            text-align: center;
            border-bottom: 2px solid #f8bbd0;
            padding-bottom: 10px;
            margin-bottom: 20px;
        }
        ul {
            list-style: none;
            padding: 0;
        }
        ul li {
            background-color: #fff8fb;
            margin-bottom: 10px;
            padding: 10px;
            border-left: 5px solid #f06292;
            border-radius: 5px;
        }
        a {
            color: #e91e63;
            text-decoration: none;
            font-weight: bold;
        }
        a:hover {
            text-decoration: underline;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>
    <div class="container">
        <h2> Hasil Data Diri dan Penghitungan Gaji</h2>
        <p>Halo, <b><?php echo htmlspecialchars($nama); ?></b>! Berikut hasil perhitungan data Anda:</p>
        <ul>
            <li><b>Tanggal Lahir:</b> <?php echo htmlspecialchars($tgl_lahir_str); ?></li>
            <li><b>Umur:</b> <?php echo $umur; ?> tahun</li>
            <li><b>Pekerjaan:</b> <?php echo htmlspecialchars($nama_pekerjaan); ?></li>
            <li><b>Estimasi Gaji:</b> <?php echo htmlspecialchars($gaji_formatted); ?></li>
        </ul>
        <p><a href="index.php"> Kembali ke Form Input</a></p>
    </div>
</body>
</html>
```
<img width="1920" height="1080" alt="Cuplikan layar 2025-11-10 133754" src="https://github.com/user-attachments/assets/89629138-273f-4955-91a7-7360f9619b6e" />


