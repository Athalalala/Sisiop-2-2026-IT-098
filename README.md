# Sisiop-2-2026-IT-098

## Profil Mahasiswa
Nama           : Jude Athala Yazid Sari

NRP            : 5027251098

Departemen     : Teknologi Informasi

Kelas          : Sistem Operasi A
 

## **Laporan Penyelesaian Soal Praktikum Modul 2**
Repository ini berisi *source code* dan penjelasan mengenai penyelesaian soal Praktikum Modul 2 untuk mata kuliah Sistem Operasi. Modul ini berfokus pada *proces & daemon* pada sistem operasi.

### Problem Keseluruhan
Pada penyelesaian Soal Modul 2 ini saya juga menggunakan bantuan Claude Ai karena di peraturan diperbolehkan menggunakan Ai. Disini saya menggunakan claude Ai untuk membuat script, menjelaskan alur dan memecahkan masalah pada penyelesaian soal Modul 2. Berikut link percakapan saya dengan Claude Ai
[Claude AI](https://claude.ai/share/5e612c0c-7d49-41bf-bd8e-2be75d92981d)

# Soal 1

## Deskripsi soal

Pada soal ini diceritakan bahwa komputer kasir milik Uncle Muthu terkena virus. Di dalamnya terdapat file buku_hutang.csv yang harus segera diamankan. Selain itu, diperlukan juga pemisahan data pelanggan dengan status "Belum Lunas" agar dapat ditindaklanjuti. `kasir_muthu.c` yang dapat melakukan serangkaian proses secara otomatis dan berurutan, mulai dari membuat folder penyimpanan, menyalin file, memproses data, hingga mengarsipkan hasilnya. Seluruh proses harus dijalankan menggunakan konsep sequential process dengan memanfaatkan `fork` , `exec`, dan `waitpid` tanpa menggunakan system.

## Penyelesaian soal 1

### Berikut langkah - langkah pengerjaan soal_1

#### langkah pertama

**inisiasi**

pertama-tama saat, karena saat mengerjakan sudah ada direktori soal_1, kita buat direktori modul_2 `mkdir modul_2` lalu masuk ke modul_2 `cd modul_2`. selanjutnya buat direktori soal_1 `mkdir soal_1`, lalu masuk soal_1 `cd soal_1` ![image link](Assets/gambar_30.png)  

![image link](Assets/gambar_31.png)

![image link](Assets/gambar_32.png)

![image link](Assets/gambar_33.png)

#### langkah kedua

mendownload spreadsheet yang sudah disediakan dengan cara `wget -O "url link"`

![image link](Assets/gambar_34.png)

setelah itu cek apakah sudah benar dengan cara `cat buku_hutang.csv`

![image link](Assets/gambar_28.png)


#### langkah ketiga

selanjutnya, saya membuat file script dengan nama kasir_muthu.c lalu diisi dengan kode script seperti dibawah ini.

`cat > kasir_muthu.c << 'EOF'
"script dari kasir_muthu.c"
'EOF'`

```awk

cat > kasir_muthu.c << 'EOF'

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

#define ERROR_MSG "[ERROR] Aiyaa! Proses gagal, file atau folder tidak ditemukan.\n"
#define SUCCESS_MSG "[INFO] Fuhh, selamat! Buku hutang dan daftar penagihan berhasil diamankan.\n"

void run_child(char *argv[]) {
    pid_t pid = fork();
    if (pid < 0) {
        perror("fork failed");
        exit(EXIT_FAILURE);
    }
    if (pid == 0) {
        execvp(argv[0], argv);
        perror("exec failed");
        exit(EXIT_FAILURE);
    } else {
        int status;
        waitpid(pid, &status, 0);
        if (!WIFEXITED(status) || WEXITSTATUS(status) != 0) {
            printf(ERROR_MSG);
            exit(EXIT_FAILURE);
        }
    }
}

void run_shell_child(const char *cmd) {
    pid_t pid = fork();
    if (pid < 0) {
        perror("fork failed");
        exit(EXIT_FAILURE);
    }
    if (pid == 0) {
        char *argv[] = {"bash", "-c", (char *)cmd, NULL};
        execvp("bash", argv);
        perror("exec failed");
        exit(EXIT_FAILURE);
    } else {
        int status;
        waitpid(pid, &status, 0);
        if (!WIFEXITED(status) || WEXITSTATUS(status) != 0) {
            printf(ERROR_MSG);
            exit(EXIT_FAILURE);
        }
    }
}

int main() {
    char *mkdir_args[] = {"mkdir", "-p", "brankas_kedai", NULL};
    run_child(mkdir_args);

    char *cp_args[] = {"cp", "buku_hutang.csv", "brankas_kedai/", NULL};
    run_child(cp_args);

    const char *grep_cmd = "grep \"Belum Lunas\" brankas_kedai/buku_hutang.csv > brankas_kedai/daftar_penunggak.txt";
    run_shell_child(grep_cmd);

    char *zip_args[] = {"zip", "-r", "rahasia_muthu.zip", "brankas_kedai/", NULL};
    run_child(zip_args);

    printf(SUCCESS_MSG);
    return 0;
'EOF'
}

```

#### langkah keempat

selanjutnya, download zip dengan perintah `sudo apt install zip -y`

![image link](Assets/gambar_38.png)

#### langkah kelima

compile zip dengan cara `gcc kasir_muthu.c

![image link](Assets/gambar_40.png)

#### langkah keenam 

jalankan dengan cara `./kasir_muthu`

![image link](Assets/gambar_41.png)

## Hasil Output

![image link](Assets/gambar_39.png)

## Problem saat pengerjaan

Pada saat pengerjaan soal_1 modul 2 ini sempat kebingungan karena ada output `503 service unavailable` saat proses install `gcc` dan `zip` tetapi lupa untuk didokumentasikan karena pada saat ingin back scroll keatas di terminal ke atas, terminal nya ngelag jadi harus di clear, saat dicoba menggunakan wifi my-its terjadi  `503 service unavailable` tetapi jika menggunakan hotspot pribadi aman aman saja.

#### perintah perintah yang ada di soal_1

`cd` digunakan untuk berpindah direktori. command `cd` dipakai untuk masuk ke folder soal_1 ataupun folder yang sesuai dengan yang diinginkan agar seluruh proses dikerjakan di lokasi yang sesuai.

`wget -O` digunakan untuk mengunduh file dari internet. File buku_hutang.csv diambil dari link yang sudah disediakan untuk kemudian digunakan dalam proses selanjutnya.

`ls` digunakan untuk melihat daftar file dan folder yang ada di dalam direktori.

`cat` berfungsi untuk menampilkan isi file ke terminal. Digunakan untuk memastikan isi buku_hutang.csv sudah benar, serta untuk melihat hasil dari file daftar_penunggak.txt.

`gcc` digunakan untuk melakukan kompilasi program C. File kasir_muthu.c diubah menjadi file "executable" agar bisa dijalankan.

`./` ditujukan untuk menjalankan file "executable" hasil kompilasi, yaitu program kasir_muthu.

`mkdir` digunakan untuk membuat direktori baru. Dalam program, perintah ini dipakai untuk membuat folder brankas_kedai.

`cp` digunakan untuk menyalin file dari satu lokasi ke lokasi lain. File buku_hutang.csv disalin ke dalam folder brankas_kedai.

`grep` digunakan untuk mencari teks tertentu di dalam file. Digunakan untuk mengambil data dengan status “Belum Lunas” dari file CSV.

`zip` ini untuk mengompres file atau folder menjadi arsip. Folder brankas_kedai kemudian dikompres menjadi file rahasia_muthu.zip.


