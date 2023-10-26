# Register, Authentication, dan Authorization

* ## Register
  <tb>1. Pastikan terdapat tabel ```users``` yang dibuat menggunakan migration pada bab 3 ___Basic Routing dan Migration___. Beikut informasi kolom yang harus ada <br>
  id |
  --- |
  createdAt |
  updatedAt |
  name |
  email |
  password |

  <tb>2. Pastikan terdapat model ```User.php``` yang digunakan pada bab 5 ___Model, Controller, dan Request-Response Handler___. Berikut baris kode yang harus ada <br>
  ```
    <?php

    namespace App\Models;
    use Illuminate\Database\Eloquent\Model;
    class User extends Model

    {
        /**
        * The attributes that are mass assignable.
        *
        * @var array
        */

        protected $fillable = [
            'name', 'email', 'password',
            'token' //
        ];

        /**
        * The attributes excluded from the model's JSON form.
        *
        * @var array
        */

        protected $hidden = [];
    }
  ```

  <tb>3. Buatlah file ```AuthController.php``` dan isilah dengan baris kode berikut <br>
  ```
    <?php
      namespace App\Http\Controllers;
  
      use App\Models\User;
      use Illuminate\Http\Request;
      use Illuminate\Support\Facades\Hash;
  
      class AuthController extends Controller
      {
        /**
        * Create a new controller instance.
        *
        * @return void
        */
        public function __construct()
        {
          //
        }
  
        //
        public function register(Request $request)
        {
          $name = $request->name;
          $email = $request->email;
          $password = Hash::make($request->password);
  
          $user = User::create([
            'name' => $name,
            'email' => $email,
            'password' => $password
          ]);
  
          return response()->json([
            'status' => 'Success',
            'message' => 'new user created',
            'data' => [
              'user' => $user,
            ]
          ],200);
        }
      }
  ```
  <tb>4. Tambahkan baris berikut pada ```routes/web.php``` <br>
  ```
    <?php
    ...
    $router->group(['prefix' => 'auth'], function () use ($router) {
      $router->post('/register', ['uses'=> 'AuthController@register']);
    });
  ```
  <tb>5. Jalankan aplikasi pada endpoint ```/auth/register``` dengan body berikut <br>
  ```
    {
      "name": "Scaramouche",
      "email": "scaramouche@fatui.org",
      "password": "wanderer"
    }
  ```
  
* ## Authentication
  Otentifikasi adalah proses untuk mengenali identitas dengan mekanisme pengasosiasian permintaan yang masuk dengan satu set kredensial pengidentifikasi. Kredensial yang diberikan akan dibandingkan dengan database informasi pengguna yang berwenang di dalam sistem operasi lokal atau server otentifikasi. <br>
  <tb>1. Buatlah fungsi ```login(Request $request)``` pada file ```AuthController.php``` <br>
  ```
    <?php
      namespace App\Http\Controllers;
  
      use App\Models\User;
      use Illuminate\Http\Request;
      use Illuminate\Support\Facades\Hash;
  
      class AuthController extends Controller
      {
        ...
        public function login(Request $request)
        {
            $email = $request->email;
            $password = $request->password;

            $user = User::where('email', $email)->first();

            if (!$user) {
                return response()->json([
                    'status' => 'Error',
                    'message' => 'user not exist',
                ],404);
            }

            if (!Hash::check($password, $user->password)) {
                return response()->json([
                    'status' => 'Error',
                    'message' => 'wrong password',
                ],400);
            }
  
            return response()->json([
                'status' => 'Success',
                'message' => 'successfully login',
                'data' => [
                    'user' => $user,
                ]
            ],200);
        }
    }
  ```
  <tb>2. Tambahkan baris berikut pada ```routes/web.php``` <br>
  ```
    <?php
    ...
    $router->group(['prefix' => 'auth'], function () use ($router) {
      $router->post('/register', ['uses'=> 'AuthController@register']);
      $router->post('/login', ['uses'=> 'AuthController@login']); // route login
    });
  ```
  <tb>3. Jalankan aplikasi pada endpoint ```/auth/login``` dengan body berikut <br>
  ```
    {
      "email": "scaramouche@fatui.org",
      "password": "wanderer"
    }
  ```
  > [!NOTE]
  > Opsional: lakukan percobaan dengan menyalahkan email dan password dan amati responnya
  
* ## Token
  Token merupakan nilai yang digunakan untuk mendapatkan akses ke sumber daya yang dibatasi secara elektronik. Penggunaan token ditujukan pada web service yang tidak menyimpan state yang berkaitan dengan penggunaan aplikasi (stateless) seperti session. <br>
  <tb>1. Jalankan perintah berikut untuk membuat migrasi baru <br>
  ```
    php artisan make:migration add_column_token_to_users
  ```
  <tb>2. Tambahkan baris berikut pada migration yang baru terbuat <br>
  ```
    <?php

      use Illuminate\Database\Migrations\Migration;
      use Illuminate\Database\Schema\Blueprint;
      use Illuminate\Support\Facades\Schema;
      
      class AddColumnTokenToUsers extends Migration
      {
          /**
           * Run the migrations.
           *
           * @return void
           */
          public function up()
          {
              Schema::table('users', function (Blueprint $table) {
                  $table->string('token', 72)->unique()->nullable(); //
              });
          }
      
          /**
           * Reverse the migrations.
           *
           * @return void
           */
          public function down()
          {
              Schema::table('users', function (Blueprint $table) {
                  $table->dropIfExists('token'); //
              });
          }
      }

  ```
  <tb>3. Jalankan aplikasi pada endpoint ```/auth/login``` dengan body berikut <br>
  <tb>3. Jalankan aplikasi pada endpoint ```/auth/login``` dengan body berikut <br>
  <tb>3. Jalankan aplikasi pada endpoint ```/auth/login``` dengan body berikut <br>
  <tb>3. Jalankan aplikasi pada endpoint ```/auth/login``` dengan body berikut <br>
* ## Authorization
