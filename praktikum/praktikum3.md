# Integrasi MongoDB dan Express

* ## Percobaan Instalasi NodeJS
  a. Buka halaman ```https://nodejs.org/en/``` <br>
  ![Screenshot node.js](../Laprak3/1.PNG) <br>
  b. Download dan jalankan node setup <br>
  c. Setelah instalasi selesai jalankan command ```node -v``` untuk memeriksa apakah NodeJS sudah terinstall <br>
  ![Screenshot node.js](../Laprak3/2.PNG) <br>
  
* ## Inisiasi Project Express dan Pemasangan Package
  Express.js merupakan sebuah framework web app untuk Node.js yang ditulis dalam bahasa pemrograman JavaScript. Express.js berfungsi untuk mengatur fungsionalitas website, seperti pengelolaan routing dan session, permintaan HTTP, penanganan error, dan pertukaran data di server. <br>

  Mongoose adalah pustaka berbasis Node.js yang digunakan untuk pemodelan data pada MongoDB. Mongoose menyediakan fitur seperti, model data application berbasis Schema yang termasuk di dalamnya built-in type casting, validation, query building, business logic hooks dan masih banyak lagi. <br>

  Inisiasi project Express.js dapat dilakukan dengan cara: <br>
  a. Lakukan pembuatan folder dengan nama express-mongodb dan masuk ke dalam folder tersebut lalu buka melalui text editor masing-masing <br>
  ![Screenshot express](../Laprak3/3.PNG) <br>
  ![Screenshot express](../Laprak3/4.PNG) <br>
  b. Lakukan npm init untuk mengenerate file package.json dengan menggunakan command ```npm init -y``` <br>
  ![Screenshot express](../Laprak3/5.PNG) <br>
  c. Lakukan instalasi express, mongoose, dan dotenv dengan menggunakan command ```npm i express mongoose dotenv``` <br>
  ![Screenshot express](../Laprak3/6.PNG) <br>
  
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
  ![Screenshot koneksi](../Laprak3/7.PNG) <br>
  c. Setelah itu coba jalankan dengan command ```node index.js``` <br>
  > [!NOTE]
  > Lakukan langkah ini untuk melakukan restart server node setiap kali melakukan perubahan pada file
  >
  ![Screenshot koneksi](../Laprak3/8.PNG) <br>
  d. Lakukan pembuatan file **.env** dan masukkan baris berikut <br>
  ```
  PORT=5000
  ```
  ![Screenshot koneksi](../Laprak3/9.PNG) <br>
  e. Ubah kode pada listening port menjadi berikut dan coba jalankan aplikasi kembali <br>
  ```
  ...

  const PORT = process.env.PORT || 8000;
  app.listen(PORT, () => {
    console.log(`Running on port ${PORT}`);
  })
  ```
  ![Screenshot koneksi](../Laprak3/10.PNG) <br>
  f. Copy connection string yang terdapat pada compas atau atlas dan paste kan pada **.env** seperti berikut <br>
  ```
  MONGO_URI=<Connection string masing-masing>
  ```
  ![Screenshot koneksi](../Laprak3/20.PNG) <br>
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
  ![Screenshot koneksi](../Laprak3/13.PNG) <br>
  h. Jalankan aplikasi kembali seperti langkah c <br>
  ![Screenshot koneksi](../Laprak3/21.PNG) <br>
  
* ## Pembuatan Routing
  Router berfungsi untuk memilah dan mengolah request url untuk kemudian diproses sesuai tujuan akhir url tersebut. Url dapat berfungsi untuk mengambil data, menampilkan sata, menghapus data, menampilkan form, dan mengolah session. <br>

  Routing dapat dibuat dengan langkah berikut: <br>
  a. Lakukan pembuatan direktori **routes** di tingkat yang sama dengan index.js <br>
  b. Buat file **book.route.js** di dalamnya <br>
  ![Screenshot routing](../Laprak3/15.PNG) <br>
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
  ![Screenshot routing](../Laprak3/16.PNG) <br>
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
  ![Screenshot routing](../Laprak3/17.PNG) <br>
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
  ![Screenshot routing](../Laprak3/18.PNG) <br>
    f. Uji salah satu endpoint dengan Postman <br>
    ![Screenshot routing](../Laprak3/22.PNG) <br>
    
* ## Pembuatan Controller
Controller merupakan bagian yang menjadi tempat berkumpulnya logika pemrograman yang digunakan untuk memisahkan organisasi data pada database. Dalam beberapa kasus, controller menjadi penghubung antara model dan view pada arsitektur MVC. <br>

Controller dapat dibuat dengan cara: <br>
a. Lakukan pembuatan direktori **controllers** di tingkat yang sama dengan index.js <br>
b. Buatlah file **book.controller.js** di dalamnya <br>
![Screenshot controller](../Laprak3/23.PNG) <br>
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
![Screenshot controller](../Laprak3/24.PNG) <br>
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
![Screenshot controller](../Laprak3/25.PNG) <br>
  e. Lakukan import book.controller.js pada file book.route.js <br>
```
  const router = require('express').Router();
  const book = require('../controllers/book.controller'); //

  ...

  module.exports = router;
```
![Screenshot controller](../Laprak3/26.PNG) <br>
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
![Screenshot controller](../Laprak3/27.PNG) <br>
  g. Lakukan pengujian kembali, pastikan response tetap sama <br>
  ![Screenshot controller](../Laprak3/28.PNG) <br>
  
* ## Pembuatan Model
  Model berfungsi untuk menyiapkan, mengatur, memanipulasi, dan mengorganisasikan data yang ada pada database. <br>

  Model dapat dibuat dengan cara: <br>
  a. Lakukan pembuatan direktori **models** di tingkat yang sama dengan index.js <br>
  b. Buat file **book.model.js** di dalamnya <br>
  ![Screenshot model](../Laprak3/29.PNG) <br>
  c. Tambahkan baris kode berikut <br>
  ```
  const mongoose = require('mongoose');
  
  const bookSchema = new mongoose.Schema({
    title: {
      type: String
    },
    author: {
      type: String
    },
    year: {
      type: Number
    },
    pages: {
      type: Number
    },
    summary: {
      type: String
    },
    publisher: {
      type: String
    }
  })
  
  module.exports = mongoose.model('book', bookSchema);
  ```
  ![Screenshot model](../Laprak3/30.PNG) <br>
  
* ## Operasi CRUD
  a. Hapus semua data pada collection books yang telah dibuat pada praktikum sebelumnya ( https://afifahrahma22.github.io/praktikum-pemin/praktikum/praktikum2 ) <br>
  ![Screenshot CRUD](../Laprak3/31.PNG) <br>
  b. Lakukan import book.model.js pada file book.controller.js <br>
  ```
  const Book = require('../models/book.model');
  
  ...
  ```
  ![Screenshot CRUD](../Laprak3/32.PNG) <br>
    c. Lakukan perubahan pada fungsi ```createBook``` <br>
  ```
  const Book = require('../models/book.model');
  
  ...
  
  async function createBook(req, res) {
    const book = new Book({
      title: req.body.title,
      author: req.body.author,
      year: req.body.year,
      pages: req.body.pages,
      summary: req.body.summary,
      publisher: req.body.publisher,
    })

    try {
      const savedBook = await book.save();
      res.status(200).json({
        message: 'membuat buku baru',
        book: savedBook,
      })
    } catch (error) {
      res.status(500).json({
        message: 'kesalahan pada server',
        error: error.message,
      })
    }
  }
  
  ...
  ```
  ![Screenshot CRUD](../Laprak3/33.PNG) <br>
    d. Buatlah dua buah buku dengan data di bawah ini dengan Postman <br>
  ```
    {
      "title": "Dilan 1990",
      "author": "Pidi Baiq",
      "year": 2014,
      "pages": 332,
      "summary": "Mirea, anata wa utsukushī",
      "publisher": "Pastel Books"
    }
  ```
  ```
    {
      "title": "Dilan 1991",
      "author": "Pidi Baiq",
      "year": 2015,
      "pages": 344,
      "summary": "Watashi ga kare o aishite iru to ittara",
      "publisher": "Pastel Books"
    }
  ```
  ![Screenshot CRUD](../Laprak3/34.PNG) <br>
  ![Screenshot CRUD](../Laprak3/35.PNG) <br>
    e. Lakukan perubahan pada fungsi ```getAllBooks``` <br>
  ```
    const Book = require('../models/book.model');
  
    async function getAllBooks(req, res) {
      try {
        const books = await Book.find();
        res.status(200).json({
          message: 'mendapatkan semua buku',
          books,
        })
      } catch (error) {
        res.status(500).json({
          message: 'kesalahan pada server',
          error: error.message,
        })
      }
    }
  
    ...
  ```
  ![Screenshot CRUD](../Laprak3/36.PNG) <br>
    f. Lakukan perubahan pada fungsi ```getOneBook``` <br>
  ```
    const Book = require('../models/book.model');
  
    ...
  
    async function getOneBook(req, res) {
      const id = req.params.id;
  
      try {
        const book = await Book.findById(id);
        res.status(200).json({
          message: 'mendapatkan satu buku',
          book,
        })
      } catch (error) {
        res.status(500).json({
          message: 'kesalahan pada server',
          error: error.message,
        })
      }
    }
  
    ...
  ```
  ![Screenshot CRUD](../Laprak3/37.PNG) <br>
    g. Tampilkan semua buku dengan Postman <br>
    ![Screenshot CRUD](../Laprak3/38.PNG) <br>
    h. Tampilkan buku Dilan 1990 dengan Postman <br>
    ![Screenshot CRUD](../Laprak3/39.PNG) <br>
    i. Lakukan perubahan pada fungsi ```updateBook``` <br>
  ```
    const Book = require('../models/book.model');
  
    ...
  
    async function updateBook(req, res) {
      const id = req.params.id;
  
      try {
        const book = await Book.findByIdAndUpdate(
          id, req.body, { new: true }
        )
        res.status(200).json({
          message: 'memperbaharui satu buku',
          book,
        })
      } catch (error) {
        res.status(500).json({
          message: 'kesalahan pada server',
          error: error.message,
        })
      }
    }
  
    ...
  ```
  ![Screenshot CRUD](../Laprak3/40.PNG) <br>
    j. Ubah judul buku Dilan 1991 menjadi “NAMA PANGGILAN 1991” dengan Postman <br>
    ![Screenshot CRUD](../Laprak3/41.PNG) <br>
    k. Lakukan perubahan pada fungsi ```deleteBook``` <br>
  ```
    const Book = require('../models/book.model');
  
    ...
  
    async function deleteBook(req, res) {
      const id = req.params.id;
  
      try {
        const book = await Book.findByIdAndDelete(id);
        res.status(200).json({
          message: 'menghapus satu buku',
          book,
        })
      } catch (error) {
        res.status(500).json({
          message: 'kesalahan pada server',
          error: error.message,
        })
      }
    }
  
    ...
  ```
  ![Screenshot CRUD](../Laprak3/42.PNG) <br>
    l. Hapus buku Dilan 1990 dengan Postman <br>
    ![Screenshot CRUD](../Laprak3/43.PNG) <br>
    ![Screenshot CRUD](../Laprak3/44.PNG) <br>
