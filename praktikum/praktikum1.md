# Instalasi Lumen, MongoDB, dan Konfigurasi APP Key

* ## Percobaan Instalasi Composer
  Instalasi composer bisa dilakukan dengan cara membuka halaman https://getcomposer.org/download/ dan menjalankan Composer-Setup.exe. Namun dalam percobaan ini, composer telah terinstall sehingga langkah ini dilewati. <br>
  ![Screenshot composer](../Laprak1/composer.png)
  
* ## Percobaan Instalasi MongoDB
  Instalasi MongoDB dilakukan dengan cara mendownload MongoDB pada halaman https://www.mongodb.com/try/download/community. Setelah itu, jalankan file mongodb-windows-x86_64-7.0.1-signed.msi dan ikuti langkah-langkah berikut: <br>
  a. Klik "Next" pada halaman welcome <br>
     ![Screenshot mongoDB](../Laprak1/1.PNG) <br>
  b. Centang "I accept the terms in the License Agreement" dan klik "Next" <br>
     ![Screenshot mongoDB](../Laprak1/2.PNG) <br>
  c. Pilih opsi "Complete" pada bagian Choose Setup Type <br>
     ![Screenshot mongoDB](../Laprak1/3.PNG) <br>
  d. Klik "Next" pada Service Configuration tanpa mengubah apapun <br>
     ![Screenshot mongoDB](../Laprak1/4.PNG) <br>
  e. Pastikan "Install MongoDB Compass" tercentang <br>
     ![Screenshot mongoDB](../Laprak1/5.PNG) <br>
  f. Klik "Install" <br>
     ![Screenshot mongoDB](../Laprak1/6.PNG) <br>
  g. Tunggu hingga tahap instalasi selesai <br>
     ![Screenshot mongoDB](../Laprak1/7.png) <br>
  h. MongoDB Compass akan terbuka secara otomatis <br>
     ![Screenshot mongoDB](../Laprak1/8.png) <br>
     ![Screenshot mongoDB](../Laprak1/9.png) <br>
     
* ## Percobaan Instalasi Lumen
  Pada percobaan ini, Instalasi Lumen dilakukan menggunakan tools Visual Studio Code dengan cara berikut:
  a. Buka folder yang telah dibuat pada Visual Studio Code <br>
  b. Buka file web.php pada direktori routes dan buat endpoint baru dengan kode sebagai berikut <br>
  > $router->get('/key', function () {
    return Str::random(32);
    }); <br>
  >
    ![Screenshot lumen](../Laprak1/web.PNG) <br>
  c. Jalankan server dengan perintah <br>
  > php -S localhost:8000 -t public <br>
  >
    ![Screenshot lumen](../Laprak1/php.png) <br>
  d. Buka browser dan jalankan "localhost:8000" untuk mengecek apakah lumen telah terinstall <br>
  e. Untuk mendapat app key buka browser dan jalankan "localhost:8000/key" <br>
    ![Screenshot lumen](../Laprak1/app_key.PNG) <br>
  f. Copy app key yang didapat pada file .env pada projek lumenapi <br>
    ![Screenshot lumen](../Laprak1/input_app_key.png) <br>

