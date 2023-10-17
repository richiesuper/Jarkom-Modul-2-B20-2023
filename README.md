# Jarkom-Modul-1-B20-2023

## Informasi Kelompok

| Nama | NRP |
| ---- | --- |
| Richie Seputro | 5025211213 |
| Dimas Aria Pujangga | 5025211212 |

## Penjelasan

1. Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive berikut

Pertama, buat topologi sesuai yang diminta pada soal.
![1a](assets/1a.png)

2. Dimas

3. Dimas

4. Dimas

5. Dimas

6. Dimas

7. Dimas

8. Dimas

9. Dimas

10. Langkah pertama, masuk ke host `Prabukusuma` untuk menyetel setting Nginx dan men-download webpage yang
    akan di-serve kepada client.
    
    Selanjutnya, buka file `/etc/nginx/sites-available/default` dan tuliskan seperti ini:
    
    ![10a](assets/10a.png)
    
    Lalu, buka file `/root/.bashrc` dan tuliskan seperti ini:

    ![10b](assets/10b.png)
    
    Setelah itu, masuk ke host `Abimanyu` dan `Wisanggeni` dan ulangi langkah-langkah di atas. Ubahlah
    port yang digunakan oleh `Abimanyu` ke `8002` dan `Wisanggeni` ke `8003`. Untuk file `/root/.bashrc`
    tetap sama dengan `Prabukusuma`.
    
    Kemudian, masuk ke host `Arjuna` dan edit file `/etc/nginx/sites-available/arjuna.b20.com` menjadi
    seperti ini:

    ![10c](assets/10c.png)
    
    Selanjutnya, tambahkan baris-baris berikut ke file `/root/.bashrc`:

    ![10d](assets/10d.png)
    
    Terakhir, kita masuk ke client host `Sadewa` dan tes website `arjuna.b20.com` dengan `lynx`:

    ![10e](assets/10e.png)

    ![10f](assets/10f.png)

    ![10g](assets/10g.png)
    
    Terlihat bahwa Load Balancer telah berhasil di-setup dan telah membagi load
    secara round-robin antara `Prabukusuma`, `Abimanyu`, dan `Wisanggeni`.

11. Pertama, masuk ke host `Abimanyu` dan edit file `/etc/apache2/sites-available/abimanyu.b20.com.conf`:

    ![11a](assets/11a.png)
    
    Kemudian, tambahkan baris-baris berikut ke file `/root/.bashrc`:

    ![11b](assets/11b.png)
    
    Terakhir, tes website `www.abimanyu.b20.com` dengan `lynx` dari host `Sadewa`:

    ![11c](assets/11c.png)
    
    Terlihat bahwa server Apache berhasil melayani request dari client.

12. Pertama, kita coba akses `www.abimanyu.b20.com/home`:

    ![12a](assets/12a.png)
    
    Terlihat bahwa server mengembalikan error code 404 Not Found.

    Kedua, kita tambahkan baris berikut ke file `/etc/apache2/sites-available/abimanyu.b20.com.conf`:

    ![12b](assets/12b.png)
    
    Baris tersebut akan membuat `/home` mengarah ke `/index.php/home`. Setelah me-restart service `apache2`, lakukan pengetesan dari host `Sadewa`:

    ![12c](assets/12c.png)
    ![12d](assets/12d.png)
    
    Terlihat bahwa sekarang `/home` sudah menghasilkan sebuah webpage.

13. Pertama, tambahkan file `/etc/apache2/sites-available/parikesit.abimanyu.b20.com.conf`:

    ![13a](assets/13a.png)
    
    Kemudian, tambahkan baris-baris berikut ke file `/root/.bashrc`:
    
    ![13b](assets/13b.png)
    
    Terakhir, cek apakah website `www.parikesit.abimanyu.b20.com` dapat diakses melalui Lynx dari host `Sadewa`:

    ![13c](assets/13c.png)
    
    Terlihat bahwa webpage berhasil ditampilkan.

14. Pertama, tambahkan directive-directive berikut ke file `/etc/apache2/sites-available/parikesit.abimanyu.b20.com.conf`:

    ![14a](assets/14a.png)
    
    Lalu, kita akan mencoba untuk membuka `/public` menggunakan Lynx:

    ![14b](assets/14b.png)
    
    Terlihat bahwa directory listing pad `/public` telah bekerja.
    
    Selanjutnya, kita akan mencoba membuka directory `/secret`:

    ![14c](assets/14c.png)
    ![14d](assets/14d.png)
    
    Terlihat bahwa server mengembalikan error code 403 Forbidden.

15. Untuk kustomisasi error page, laman error kustom-nya telah diberikan dari file zip yang disediakan.
    Kita hanya perlu menetapkan kedua file laman error tersebut untuk digunakan ketika terjadi kode error 403 dan 404.
    
    Ubah file `/etc/apache2/sites-available/parikesit.abimanyu.b20.com.conf` dan tambahkan directive-directive berikut:

    ![15a](assets/15a.png)
    
    Kemudian cobalah untuk mengakses laman-laman yang tidak ada maupun yang dilarang untuk diakses, contohnya sebagai berikut:

    Kasus kode error 404 Not Found:
    
    ![15b](assets/15b.png)
    ![15c](assets/15c.png)

    Kasus kode error 403 Forbidden:
    ![15d](assets/15d.png)
    ![15e](assets/15e.png)

16. Pertama, tambahkan directive berikut ke file `/etc/apache2/sites-available/parikesit.abimanyu.b20.com.conf`:

    ![16a](assets/16a.png)
    
    Setelah itu, cek apakah `/js` sudah dapat diakses dan mengarah ke `/public/js` dari client `Sadewa`:

    ![16b](assets/16b.png)
    
    Terlihat bahwa memang benar `/js` sudah menjadi alias `/public/js`.

17. Pertama, tambahkan baris-baris command berikut ke `/root/.bashrc`:

    ![17](assets/17.png)

    Selanjutnya, tambahkan file `/etc/apache2/sites-available/rjp.baratayuda.abimanyu.b20.com.conf` yang berisi:

    ![17a](assets/17a.png)
    
    Perhatikan bagian atas. Terdapat pengaturan bahwa VirtualHost akan melakukan listening di port 14000 dan 14400.
    
    Kemudian, jangan lupa untuk menambahkan directive untuk listening di port 14000 dan 14400 ke file `/etc/apache2/ports.conf`:

    ![17b](assets/17b.png)
    
    Terakhir, kita akan mengecek dengan cara mengakses `rjp.baratayuda.abimanyu.b20.com` melalui port 80. Seharusnya
    permintaan tersebut tidak akan menampilkan webpage yang sesungguhnya.
    
    ![17c](assets/17c.png)
    ![17d](assets/17d.png)
    
    Terlihat bahwa request ke laman yang benar gagal karena server tidak melakukan listening untuk request di port 80
    untuk subdomain `rjp.baratayuda.abimanyu.b20.com`.

    Namun, jika kita coba di port 14000 dan 14400, maka akan tampil laman website-nya:

    ![17e](assets/17e.png)
    ![17f](assets/17f.png)

    ![17g](assets/17g.png)
    ![17h](assets/17h.png)

18. Pertama, tambahkan directive berikut ke file `/etc/apache2/sites-available/rjp.baratayuda.abimanyu.b20.com.conf`:

    ![18a](assets/18a.png)
    
    Selanjutnya, tambahkan command berikut ke `/root/.bashrc`:
    
    ![18b](assets/18b.png)
    
    Lalu, kita akan mencoba untuk mengakses laman `rjp.baratayuda.abimanyu.b20.com`:
    
    ![18c](assets/18c.png)
    ![18d](assets/18d.png)
    
    Terlihat bahwa akses tanpa otorisasi ditolak oleh server.
    
    Masukkan username dan password yang telah ditentukan sebelumnya:

    ![18e](assets/18e.png)
    ![18f](assets/18f.png)
    
    Jika kredensial benar, akan tampil laman yang kita inginkan:

    ![18g](assets/18g.png)

19. Pertama, tambahkan file `/var/www/abimanyu.b20/.htaccess` yang berisikan:

    ![19a](assets/19a.png)
    
    Kemudian, jangan lupa untuk menambahkan directive berikut pada `/etc/apache2/sites-available/abimanyu.b20.com.conf` agar perubahan yang dilakukan dalam file `.htaccess` dapat dijalankan:

    ![19b](assets/19b.png)

20. Pertama, tambahkan file `/var/www/parikesit.abimanyu.b20/.htaccess` yang berisikan:

    ![20a](assets/20a.png)

    Kemudian, tambahkan directive berikut ke `/etc/apache2/sites-available/parikesit.abimanyu.b20.com.conf`:

    ![20b](assets/20b.png)
    
    Selanjutnya, kita akan mencoba meng-query gambar yang tidak mengandung substring `abimanyu`.

    ![20c](assets/20c.png)
    ![20d](assets/20d.png)
    
    Terlihat bahwa link tetap seperti semula, tidak terjadi redirect apapun.

    Namun, ketika kita mencoba lagi dengan query yang mengandung substring `abimanyu`, maka akan di-redirect ke gambar `abimanyu.png`:
    
    ![20e](assets/20e.png)
