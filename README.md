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

#### Berikut langkah - langkah pengerjaan soal_1



## Hasil Output


## Problem saat pengerjaan

Pada saat pengerjaan soal_1 modul 2 ini sempat kebingungan karena ada output `503 service unavailable` saat proses install `gcc` dan `zip`


# Soal 2

## Deskripsi soal

Soal kedua mengangkat konsep proses yang berjalan di latar belakang atau daemon, yang dianalogikan dengan kehidupan yang terus berjalan meskipun tidak selalu terlihat. Dalam soal ini, diminta untuk membuat program daemon bernama contract_daemon.c yang mampu berjalan secara terus-menerus di background. Program ini harus dapat membuat file contract.txt, menjaga keutuhan isi file tersebut, serta mencatat aktivitas ke dalam file log secara berkala. Selain itu, program juga harus mampu merespon ketika file dihapus atau diubah, serta memberikan pesan khusus ketika proses dihentikan.

## Penyelesaian soal_2

#### Berikut langkah - langkah pengerjaan soal_2






selanjutnya, saya membuat file script dengan nama kasir_muthu.c yang berisi kode script dibawah ini.
```awk

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
}

```



## Hasil Output


## Problem saat pengerjaan

Pada saat pengerjaan soal_1 modul 2 ini sempat kebingungan karena ada output `503 service unavailable` saat proses install `gcc` dan `zip`


# Soal 2

## Deskripsi soal

Pada soal ini diceritakan bahwa komputer kasir milik Uncle Muthu terkena virus. Di dalamnya terdapat file buku_hutang.csv yang harus segera diamankan. Selain itu, diperlukan juga pemisahan data pelanggan dengan status "Belum Lunas" agar dapat ditindaklanjuti. `kasir_muthu.c` yang dapat melakukan serangkaian proses secara otomatis dan berurutan, mulai dari membuat folder penyimpanan, menyalin file, memproses data, hingga mengarsipkan hasilnya. Seluruh proses harus dijalankan menggunakan konsep sequential process dengan memanfaatkan `fork` , `exec`, dan `waitpid` tanpa menggunakan system.

## Penyelesaian soal 2

#### Berikut langkah - langkah pengerjaan soal_2



## Hasil Output


## Problem saat pengerjaan

Pada saat pengerjaan soal_1 modul 2 ini sempat kebingungan karena ada output `503 service unavailable` saat proses install `gcc` dan `zip`

