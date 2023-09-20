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
  Router berfungsi untuk memilah dan mengolah request url untuk kemudian diproses sesuai tujuan akhir url tersebut. Url dapat berfungsi untuk mengambil data, menampilkan sata, menghapus data, menampilkan form, dan mengolah session. <br>

  Routing dapat dibuat dengan langkah berikut: <br>
  a. Lakukan pembuatan direktori **routes** di tingkat yang sama dengan index.js <br>
  b. Buat file **book.route.js** di dalamnya <br>
  c. Tambahkan baris kode berikut untuk fungsi ```getAllBooks``` <br>
  ```
  const router = require('express').Router();
  
  router.get('/', function getAllBooks(req, res) {
    res.status(200).json({
      message: 'mendapatkan semua buku'
    })
  })
  module.exports = router;
  ```
    d. Lakukan hal yang sama untuk ```getOneBook```, ```createBook```, ```updateBook```, dan ```deleteBook``` <br>
  ```
  const router = require('express').Router();
  
  ...
  
  router.get('/:id', function getOneBook(req, res) {
    const id = req.params.id;
    res.status(200).json({
      message: 'mendapatkan satu buku',
      id,
    })
  })

  router.post('/', function createBook(req, res) {
    res.status(200).json({
      message: 'membuat buku baru'
    })
  })

  router.put('/:id', function updateBook(req, res) {
    const id = req.params.id;
    res.status(200).json({
      message: 'memperbaharui satu buku',
      id,
    })
  })
  
  router.delete('/:id', function deleteBook(req, res) {
  const id = req.params.id;
    res.status(200).json({
      message: 'menghapus satu buku',
      id,
    })
  })
  
  module.exports = router;
  ```
    e. Lakukan import book.route.js pada file index.js dan tambahkan baris kode berikut <br>
  ```
  require('dotenv').config();
  const express = require('express');
  const mongoose = require('mongoose');
  
  const bookRoutes = require('./routes/book.route'); //
  
  ...
  
  app.get('/', (req, res) => {
    res.status(200).json({
      message: '<nama>,<nim>'
    })
  })
  
  app.use('/books', bookRoutes); //
  
  const PORT = process.env.PORT || 8000;
  app.listen(PORT, () => {
    console.log(`Running on port ${PORT}`);
  })
  ```
    f. Uji salah satu endpoint dengan Postman <br>
    
* ## Pembuatan Controller
Controller merupakan bagian yang menjadi tempat berkumpulnya logika pemrograman yang digunakan untuk memisahkan organisasi data pada database. Dalam beberapa kasus, controller menjadi penghubung antara model dan view pada arsitektur MVC. <br>

Controller dapat dibuat dengan cara: <br>
a. Lakukan pembuatan direktori **controllers** di tingkat yang sama dengan index.js <br>
b. Buatlah file **book.controller.js** di dalamnya <br>
c. Salin baris kode dari routes untuk fungsi ```getAllBooks``` <br>
```
function getAllBooks(req, res) {
  res.status(200).json({
    message: 'mendapatkan semua buku'
  })
};

module.exports = {
  getAllBooks,
}
```
  d. Lakukan hal yang sama untuk ```getOneBook```, ```createBook```, ```updateBook```, dan ```deleteBook``` <br>
```
...

function getOneBook(req, res) {
  const id = req.params.id;
  res.status(200).json({
    message: 'mendapatkan satu buku',
    id,
  })
}

function createBook(req, res) {
  res.status(200).json({
    message: 'membuat buku baru'
  })
}

function updateBook(req, res) {
  const id = req.params.id;
  res.status(200).json({
    message: 'memperbaharui satu buku',
    id,
  })
}

function deleteBook(req, res) {
  const id = req.params.id;
  res.status(200).json({
    message: 'menghapus satu buku',
    id,
  })
}

module.exports = {
getAllBooks,
getOneBook, //
createBook, //
updateBook, //
deleteBook //
}
```
  e. Lakukan import book.controller.js pada file book.route.js <br>
```
  const router = require('express').Router();
  const book = require('../controllers/book.controller'); //

  ...

  module.exports = router;
```
  f. Lakukan perubahan pada fungsi agar dapat memanggil fungsi dari book.controller.js <br>
```
const router = require('express').Router();
const book = require('../controllers/book.controller');

router.get('/', book.getAllBooks);
router.get('/:id', book.getOneBook);
router.post('/', book.createBook);
router.put('/:id', book.updateBook);
router.delete('/:id', book.deleteBook);

module.exports = router;
```
  g. Lakukan pengujian kembali, pastikan response tetap sama <br>
  
* ## Pembuatan Model
* ## Operasi CRUD

