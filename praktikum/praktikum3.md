# Integrasi MongoDB dan Express

* ## Percobaan Instalasi NodeJS
  a. Buka halaman ```https://nodejs.org/en/``` <br>
  b. Download dan jalankan node setup <br>
  c. Setelah instalasi selesai jalankan command ```node -v``` untuk memeriksa apakah NodeJS sudah terinstall <br>
  
* ## Inisiasi Project Express dan Pemasangan Package
  Express.js merupakan sebuah framework web app untuk Node.js yang ditulis dalam bahasa pemrograman JavaScript. Express.js berfungsi untuk mengatur fungsionalitas website, seperti pengelolaan routing dan session, permintaan HTTP, penanganan error, dan pertukaran data di server. <br>

  Mongoose adalah pustaka berbasis Node.js yang digunakan untuk pemodelan data pada MongoDB. Mongoose menyediakan fitur seperti, model data application berbasis Schema yang termasuk di dalamnya built-in type casting, validation, query building, business logic hooks dan masih banyak lagi. <br>

  Inisiasi project Express.js dapat dilakukan dengan cara: <br>
  a. Lakukan pembuatan folder dengan nama express-mongodb dan masuk ke dalam folder tersebut lalu buka melalui text editor masing-masing <br>
  b. Lakukan npm init untuk mengenerate file package.json dengan menggunakan command ```npm init -y``` <br>
  c. Lakukan instalasi express, mongoose, dan dotenv dengan menggunakan command ```npm i express mongoose dotenv``` <br>
  
* ## Koneksi Express ke MongoDB
  a. Buatlah file **index.js** pada root folder <br>
  b. Masukkan kode berikut pada file **index.js** <br>
 ```
  require('dotenv').config();
  const express = require('express');
  const mongoose = require('mongoose');

  const app = express();

  app.use(express.json());

  app.get('/', (req, res) => {
    res.status(200).json({
      message: '<nama>,<nim>'
    })
  })

  const PORT = 8000;
  app.listen(PORT, () => {
    console.log(`Running on port ${PORT}`);
  })
 ```
  c. Setelah itu coba jalankan dengan command ```node index.js``` <br>
  > [!NOTE]
  > Lakukan langkah ini untuk melakukan restart server node setiap kali melakukan perubahan pada file
  > 
  d. Lakukan pembuatan file **.env** dan masukkan baris berikut <br>
  ```
  PORT=5000
  ```
  e. Ubah kode pada listening port menjadi berikut dan coba jalankan aplikasi kembali <br>
  ```
  ...

  const PORT = process.env.PORT || 8000;
  app.listen(PORT, () => {
    console.log(`Running on port ${PORT}`);
  })
  ```
  f. Copy connection string yang terdapat pada compas atau atlas dan paste kan pada **.env** seperti berikut <br>
  ```
  MONGO_URI=<Connection string masing-masing>
  ```
  g. Tambahkan baris kode berikut pada file **index.js** <br>
  ```
  require('dotenv').config();
  const express = require('express');
  const mongoose = require('mongoose');

  mongoose.connect(process.env.MONGO_URI);
  const db = mongoose.connection;

  db.on('error', (error) => {
    console.log(error);
  });

  db.once('connected', () => {
    console.log('Mongo connected');
  })

  ...
  ```
  h. Jalankan aplikasi kembali seperti langkah c <br>
  
* ## Pembuatan Routing
* ## Pembuatan Controller
* ## Pembuatan Model
* ## Operasi CRUD

