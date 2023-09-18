# CRUD MongoDB Compass dan Shell

* ## MongoDB Compass
  MongoDB Compass adalah tool berbasis Graphical User Interface (GUI) yang digunakan untuk melakukan aktivitas dasar CREATE, READ, UPDATE, dan DELETE (CRUD) tanpa commad line pada MongoDB. Berikut adalah langkah-langkah untuk melakukan CRUD pada MongoDB Compass: <br>
  a. Lakukan koneksi ke MongoDB menggunakan connection string <br>
     ![Screenshot connection](../Laprak2/1.PNG) <br>
  b. Buat database baru dengan menekan tanda plus "+", maka MongoDB Compass akan menampilkan input form seperti di bawah <br>
     ![Screenshot new database](../Laprak2/2.PNG) <br>
  c. Isi informasi yang ada dan klik "Create Database". Database baru akan dibuat oleh MongoDB Compass <br>
     ![Screenshot new database](../Laprak2/3.PNG) <br>
  c. Pada percobaan ini, proses CREATE dilakukan dengan insert buku pertama dengan melakukan klik "Add Data", pilih "Insert Document", <br>
     ![Screenshot create](../Laprak2/4.PNG) <br>
  isi dengan data yang diinginkan dan klik "Next" <br>
     ![Screenshot create](../Laprak2/5.PNG) <br>
  d. Lakukan insert buku kedua dengan cara yang sama <br>
     ![Screenshot create](../Laprak2/6.PNG) <br>
  e. Proses READ dilakukan dengan cara mencari buku dengan author "Osamu Dazai" dengan mengisi filter yang diinginkan dan klik "Find" <br>
     ![Screenshot read](../Laprak2/7.PNG) <br>
     ![Screenshot read](../Laprak2/8.PNG) <br>
  f. Sedangkan untuk proses UPDATE, dilakukan perubahan summary pada buku "No Longer Human" menjadi "Buku yang bagus (NAMA,NIM) dengan melakukan klik "Edit Document" (berlambang pensil), mengisi nilai summary yang baru, dan melakukan klik "Update" <br>
     ![Screenshot update](../Laprak2/9.PNG) <br>
     ![Screenshot update](../Laprak2/10.PNG) <br>
  g. Proses DELETE, dilakukan dengan cara penghapusan pada buku "I Am a Cat" dengan melakukan klik "Remove Document" (berlambang tong sampah) dan melakukan klik "Delete" <br>
     ![Screenshot delete](../Laprak2/11.PNG) <br>
     
* ## MongoDB Shell
  MongoDB Shell merupakan tool untuk melakukan aktivitas CRUD yang berbasis Command Line Interface (CLI). MongoDB Shell dapat diakses langsung dari MongoDB Compass atau menggunakan perintah mongosh pada Command Prompt. Berikut adalah langkah-langkah untuk melakukan CRUD pada MongoDB Shell: <br>
  a. Lakukan koneksi ke MongoDB dengan menjalankan command ```mongosh``` pada terminal yang ada di OS <br>
     ![Screenshot mongosh](../Laprak2/12.PNG) <br>
  b. Lihat list database yang ada di server dengan menjalankan command ```show dbs``` <br>
     ![Screenshot show dbs](../Laprak2/13.PNG) <br>
    Untuk berpindah ke database "bookstore" gunakan command ```use bookstore``` dan memastikan database telah berpindah dengan melihat tulisan sebelum tanda ">" <br>
     ![Screenshot use bookstore](../Laprak2/14.PNG) <br>
  Untuk melihat collection yang ada pada database tersebut gunakan command ```show collection``` <br>
     ![Screenshot show collection](../Laprak2/15.PNG) <br>
  c. Proses CREATE pada MongoDB Shell dapat dilakukan secara satu per satu atau langsung membuat banyak. Untuk membuat objek baru, dilakukan insert buku "Overlord I" dengan menggunakan command ```db.books.insertOne(data)``` <br>
     ![Screenshot create](../Laprak2/16.PNG) <br>
  d. Sementara untuk membuat objek baru lebih dari satu, dilakukan insert buku "The Setting Sun" dan "Hujan" dengan insert many dengan menggunakan command ```db.books.insertMany(data)``` <br>
     ![Screenshot create](../Laprak2/17.PNG) <br>
  e. Aktivitas READ, dilakukan dengan pencarian buku dengan menggunakan command ```db.books.find()``` untuk melakukan pencarian semua buku <br>
     ![Screenshot read](../Laprak2/18.PNG) <br>
  f. Tampilkan seluruh buku dengan author "Osamu Dazai" dengan mengisi argument pada find() dengan menggunakan command ```db.books.find({filter})``` <br>
     ![Screenshot read](../Laprak2/19.PNG) <br>
  g. Proses UPDATE dapat dilakukan dengan melakukan perubahan summary pada buku "Hujan" menjadi "Buku yang bagus (NAMA, NIM) dengan menggunakan command ```db.books.updateOne({filter}, {$set: {data yang ingin diupdate}})``` <br>
     ![Screenshot update](../Laprak2/20.PNG) <br>
  h. Lakukan perubahan publisher menjadi "Yen Press" pada semua buku "Osamu Dazai" dengan menggunakan command ```db.books.updateMany({filter}, {$set: {data yang ingin diupdate}})``` <br>
     ![Screenshot update](../Laprak2/21.PNG) <br>
  i. Proses DELETE, dilakukan dengan penghapusan pada buku "Overlord I" dengan menggunakan command ```db.books.deleteOne({argument})``` <br>
     ![Screenshot delete](../Laprak2/22.PNG) <br>
  j. Lakukan penghapusan pada semua buku "Osamu Dazai" dengan menggunakan command ```db.books.deleteMany({argument})``` <br>
     ![Screenshot delete](../Laprak2/23.PNG) <br>
Untuk melihat hasil dari proses CRUD di atas, dapat dilakukan pencarian seluruh buku menggunakan command ```db.books.find()```
     ![Screenshot delete](../Laprak2/24.PNG) <br>
