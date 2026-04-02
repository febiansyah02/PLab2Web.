# Praktikum 2: Implementasi CRUD pada Framework CodeIgniter 4

Repositori ini berisi hasil Praktikum Pemrograman Web 2 yang fokus pada pengembangan aplikasi portal berita sederhana dengan fitur CRUD (Create, Read, Update, Delete) menggunakan CodeIgniter 4.

 
*Tujuan Praktikum*

- Memahami konsep dasar Model dalam arsitektur MVC.

- Memahami konsep dasar operasi CRUD pada database.

- Mampu membangun aplikasi web fungsional menggunakan CodeIgniter 4.

*Persiapan Lingkungan Kerja*

- Web Server: Apache & MySQL via XAMPP.

- Editor: Visual Studio Code.

- Framework: CodeIgniter 4 yang sudah terpasang di direktori lab7_php_ci.

*Struktur Basis Data*

Project ini menggunakan database lab_ci4 dengan tabel artikel yang memiliki struktur sebagai berikut:

SQL 

CREATE TABLE artikel (

    id INT(11) auto_increment,
    judul VARCHAR(200) NOT NULL,
    isi TEXT,
    gambar VARCHAR(200),
    status TINYINT (1) DEFAULT 0,
    slug VARCHAR(200),
    PRIMARY KEY(id)
);

# Langkah-Langkah Pengembangan

1. Konfigurasi Database

   Koneksi database dikonfigurasi melalui file .env dengan mengatur hostname, nama database, username, dan password.

2. Pembuatan Model (app/Models/ArtikelModel.php)

   Model berfungsi untuk berinteraksi langsung dengan tabel artikel. Di sini kita mendefinisikan $allowedFields agar data dapat diinput ke database.

3. Pengembangan Controller (app/Controllers/Artikel.php)

   Controller ini mengatur logika bisnis aplikasi, meliputi:

   - index(): Menampilkan daftar artikel untuk publik.
  
   - view($slug): Menampilkan detail artikel berdasarkan slug.
  
   - admin_index(): Mengelola daftar artikel di halaman admin.
  
   - add(): Form dan logika tambah data.
  
   - edit($id): Form dan logika pembaruan data.
  
   - delete($id): Logika penghapusan data.


4. Sistem Routing (app/Config/Routes.php)

   Pengaturan URL untuk membedakan halaman publik dan halaman administrasi:

PHP

$routes->get('/artikel/(:any)', 'Artikel::view/$1');

$routes->group('admin', function($routes) {

$routes->get('artikel', 'Artikel::admin_index');

$routes->add('artikel/add', 'Artikel::add');

$routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');

$routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');

});

# Tampilan Aplikasi

*Halaman Publik*
<img width="1919" height="1079" alt="Cuplikan layar 2026-04-02 130247" src="https://github.com/user-attachments/assets/099a4d82-7a73-44a4-97eb-c77fe2141958" />


*Halaman Detail*

*Halaman Admin (Dashboard)*
<img width="1919" height="1074" alt="Cuplikan layar 2026-04-02 130220" src="https://github.com/user-attachments/assets/1917063c-da0d-4d03-8ba6-4f076da93b82" />
