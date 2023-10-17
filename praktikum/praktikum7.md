# Relasi One-to-Many dan Many-to-Many

* ## Pembuatan Tabel
  <tb>1. Pastikan server database aktif kemudian pastikan sudah membuat database dengan nama ```lumenpost```<br>
  <tb>2. Ubah konfigurasi database pada file ```.env``` menjadi<br>
  ```
    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=lumenpost
    DB_USERNAME=root
    DB_PASSWORD=
  ```
  <tb>3. Hidupkan beberapa library bawaan dari lumen dengan membuka file ```app.php``` pada folder ```bootstrap``` dan mengubah baris berikut<br>
  ```
    // $app->withFacades();
    // $app->withEloquent();
  ```
  menjadi
  ```
    $app->withFacades();
    $app->withEloquent();
  ```
  <tb>4. Buat file ```migration``` dengan menjalankan command berikut<br>
  ```
    php artisan make:migration create_posts_table
    php artisan make:migration create_comments_table
    php artisan make:migration create_tags_table
    php artisan make:migration create_post_tag_table
  ```
  <tb>5. Ubah fungsi ```up()``` pada file ```migrasi create_posts_table```<br>
  ```
    #sebelumnya
    ...
    public function up()
    {
      Schema::create('posts', function (Blueprint $table) {
        $table->id();
        $table->timestamps();
      });
    }
    ...

    #diubah menjadi
    ...
    public function up()
    {
      Schema::create('posts', function (Blueprint $table) {
        $table->id();
        $table->timestamps();
        $table->string('content');
      });
    }
    ...
  ```
  <tb>6. Ubah fungsi ```up()``` pada file ```create_comments_table```<br>
  ```
    #sebelumnya
    ...
    public function up()
    {
      Schema::create('comments', function (Blueprint $table) {
        $table->id();
        $table->timestamps();
      });
    }
    ...
  
    #diubah menjadi
    ...
    public function up()
    {
      Schema::create('comments', function (Blueprint $table) {
        $table->id();
        $table->timestamps();
        $table->string('review');
        $table->foreignId('postId')->unsigned();
      });
    }
    ... 
  ```
  <tb>7. Ubah fungsi ```up()``` pada file ```create_tags_table```<br>
  ```
  ```
  <tb>8. Ubah fungsi ```up()``` pada file ```create_post_tag_table```<br>
  ```
  ```
* ## Pembuatan Model
* ## Relasi One-to-Many
* ## Relasi Many-to-Many
