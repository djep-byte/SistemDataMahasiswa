# Tugas Pemrograman Berbasis Kerangka Kerja (PBKK) W2
## HelloWorld!
### Langkah Pengerjaan
Jalankan code berikut secara berurutan pada terminal
```
dotnet new console -n HelloWorld
cd HelloWorld
dotnet run 
```
### Dokumentasi Hasil Run
![Hasil Run](./DataMahasiswa/images/HelloWorld.png)

## Sistem Data Mahasiswa
### Langkah Pengerjaan
Jalankan code berikut secara berurutan pada terminal
```
dotnet new console -n DataMahasiswa
cd DataMahasiswa
code .
```
Buka File Program.cs dan isi dengan code berikut
```
using System;
using System.Collections.Generic;

namespace DataMahasiswa
{
    // Class untuk merepresentasikan data mahasiswa
    class Mahasiswa
    {
        public string NIM { get; set; }
        public string Nama { get; set; }
        public string Prodi { get; set; }
        public double IPK { get; set; }

        // Constructor
        public Mahasiswa(string nim, string nama, string prodi, double ipk)
        {
            NIM = nim;
            Nama = nama;
            Prodi = prodi;
            IPK = ipk;
        }
    }

    class Program
    {
        // List untuk menyimpan data mahasiswa
        static List<Mahasiswa> daftarMahasiswa = new List<Mahasiswa>();

        static void Main(string[] args)
        {
            int pilihan;
            do
            {
                TampilkanMenu();
                Console.Write("Pilihan: ");
                
                string input = Console.ReadLine() ?? string.Empty;
                
                if (!int.TryParse(input, out pilihan))
                {
                    pilihan = 0;
                }
                
                Console.WriteLine();
                
                switch (pilihan)
                {
                    case 1:
                        TambahMahasiswa();
                        break;
                    case 2:
                        TampilkanMahasiswa();
                        break;
                    case 3:
                        CariMahasiswa();
                        break;
                    case 4:
                        HapusMahasiswa();
                        break;
                    case 5:
                        Console.WriteLine("Terima kasih telah menggunakan program.");
                        break;
                    default:
                        Console.WriteLine("Pilihan tidak tersedia!");
                        break;
                }
                
                if (pilihan != 5)
                {
                    Console.WriteLine();
                    Console.WriteLine("Tekan ENTER untuk melanjutkan...");
                    Console.ReadLine();
                }
            } while (pilihan != 5);
        }

        // =========================
        // METHOD MENAMPILKAN MENU
        // =========================
        static void TampilkanMenu()
        {
            Console.Clear();
            Console.WriteLine("========================================");
            Console.WriteLine(" SISTEM DATA MAHASISWA");
            Console.WriteLine("========================================");
            Console.WriteLine("1. Tambah Mahasiswa");
            Console.WriteLine("2. Tampilkan Mahasiswa");
            Console.WriteLine("3. Cari Mahasiswa");
            Console.WriteLine("4. Hapus Mahasiswa");
            Console.WriteLine("5. Keluar");
            Console.WriteLine("========================================");
        }

        // =========================
        // METHOD TAMBAH MAHASISWA
        // =========================
        static void TambahMahasiswa()
        {
            Console.Clear();
            Console.WriteLine("========================================");
            Console.WriteLine(" TAMBAH MAHASISWA");
            Console.WriteLine("========================================");
            
            Console.Write("NIM : ");
            string nim = Console.ReadLine() ?? string.Empty;
            
            Console.Write("Nama : ");
            string nama = Console.ReadLine() ?? string.Empty;
            
            Console.Write("Program Studi: ");
            string prodi = Console.ReadLine() ?? string.Empty;
            
            double ipk;
            while (true)
            {
                Console.Write("IPK: ");
                if (double.TryParse(Console.ReadLine(), out ipk))
                {
                    if (ipk >= 0 && ipk <= 4)
                    {
                        break;
                    }
                }
                Console.WriteLine("IPK harus berupa angka 0-4.");
            }
            
            Mahasiswa mahasiswa = new Mahasiswa(nim, nama, prodi, ipk);
            daftarMahasiswa.Add(mahasiswa);
            
            Console.WriteLine();
            Console.WriteLine("Data mahasiswa berhasil ditambahkan.");
        }

        // =========================
        // METHOD MENAMPILKAN DATA
        // =========================
        static void TampilkanMahasiswa()
        {
            Console.Clear();
            Console.WriteLine("========================================");
            Console.WriteLine(" DAFTAR MAHASISWA");
            Console.WriteLine("========================================");
            
            if (daftarMahasiswa.Count == 0)
            {
                Console.WriteLine("Belum ada data mahasiswa.");
                return;
            }
            
            Console.WriteLine("{0,-12} {1,-20} {2,-20} {3,5}", "NIM", "Nama", "Prodi", "IPK");
            Console.WriteLine("------------------------------------------------------------");
            
            foreach (Mahasiswa m in daftarMahasiswa)
            {
                Console.WriteLine("{0,-12} {1,-20} {2,-20} {3,5:F2}", m.NIM, m.Nama, m.Prodi, m.IPK);
            }
            Console.WriteLine();
        }

        // =========================
        // METHOD MENCARI MAHASISWA
        // =========================
        static void CariMahasiswa()
        {
            Console.Clear();
            Console.WriteLine("========================================");
            Console.WriteLine(" CARI MAHASISWA");
            Console.WriteLine("========================================");
            
            Console.Write("Masukkan NIM: ");
            string nimCari = Console.ReadLine() ?? string.Empty;
            
            Mahasiswa? mahasiswaDitemukan = null;
            
            foreach (Mahasiswa m in daftarMahasiswa)
            {
                if (m.NIM.Equals(nimCari, StringComparison.OrdinalIgnoreCase))
                {
                    mahasiswaDitemukan = m;
                    break;
                }
            }
            
            Console.WriteLine();
            
            if (mahasiswaDitemukan != null)
            {
                Console.WriteLine("Data ditemukan!");
                Console.WriteLine("NIM: " + mahasiswaDitemukan.NIM);
                Console.WriteLine("Nama: " + mahasiswaDitemukan.Nama);
                Console.WriteLine("Prodi: " + mahasiswaDitemukan.Prodi);
                Console.WriteLine("IPK: " + mahasiswaDitemukan.IPK.ToString("F2"));
            }
            else
            {
                Console.WriteLine("Mahasiswa dengan NIM tersebut tidak ditemukan.");
            }
        }

        // =========================
        // METHOD MENGHAPUS MAHASISWA
        // =========================
        static void HapusMahasiswa()
        {
            Console.Clear();
            Console.WriteLine("========================================");
            Console.WriteLine(" HAPUS MAHASISWA");
            Console.WriteLine("========================================");
            
            Console.Write("Masukkan NIM: ");
            string nimHapus = Console.ReadLine() ?? string.Empty;
            
            Mahasiswa? mahasiswaDitemukan = null;
            
            foreach (Mahasiswa m in daftarMahasiswa)
            {
                if (m.NIM.Equals(nimHapus, StringComparison.OrdinalIgnoreCase))
                {
                    mahasiswaDitemukan = m;
                    break;
                }
            }
            
            if (mahasiswaDitemukan != null)
            {
                daftarMahasiswa.Remove(mahasiswaDitemukan);
                Console.WriteLine();
                Console.WriteLine("Data mahasiswa berhasil dihapus.");
            }
            else
            {
                Console.WriteLine();
                Console.WriteLine("Data mahasiswa tidak ditemukan.");
            }
        }
    }
}
```
Save (ctrl + s) dan run dengan
```
dotnet run
```
### Dokumentasi Hasil Run
![Hasil Run](./DataMahasiswa/images/SistemDataMahasiswa.png)
### Dokumentasi Tambah Data Mahasiswa 1
![Data_Mahasiswa_1](./DataMahasiswa/images/Tambah1.png)
### Dokumentasi Tambah Data Mahasiswa 2
![Data_Mahasiswa_2](./DataMahasiswa/images/Tambah2.png)
### Dokumentasi Tampilkan Data
![Tampilkan_Data](./DataMahasiswa/images/Tampilkan.png)
### Dokumentasi Cari Data (berhasil)
![Cari_Data](./DataMahasiswa/images/Cari1.png)
### Dokumentasi Cari Data (gagal)
![Cari_Data_gagal](./DataMahasiswa/images/Cari2.png)
### Dokumentasi Hapus Data (berhasil)
![Hapus_Data_berhasil](./DataMahasiswa/images/Hapus1.png)
### Dokumentasi Data Setelah Dihapus
![Data_Baru](./DataMahasiswa/images/Hapus2.png)
### Dokumentasi Keluar
![Keluar](./DataMahasiswa/images/Keluar.png)
