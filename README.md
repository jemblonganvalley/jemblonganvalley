---


---

<h1 id="mysql-basic">MYSQL BASIC</h1>
<p><img src="https://images.pexels.com/photos/1148820/pexels-photo-1148820.jpeg?auto=compress&amp;cs=tinysrgb&amp;dpr=2&amp;w=500" alt="mysql"><br>
<small>image courtesy : <a href="https://www.pexels.com/@cookiecutter">https://www.pexels.com/@cookiecutter</a></small></p>
<p><em>Menurut <a href="https://www.hostinger.co.id/tutorial/apa-itu-mysql">Hostinger.co.id</a></em>,</p>
<blockquote>
<p>MySQL adalah sistem manajemen database relasional open source (RDBMS) dengan client-server model. Sedangkan <a href="https://en.wikipedia.org/wiki/Relational_database_management_system">RDBMS</a> merupakan software untuk membuat dan mengelola database berdasarkan pada model relasional.</p>
</blockquote>
<p>Sebelum dibahas lebih lanjut, ada baiknya bagi kita untuk mengetahui sejarah singkat MySQL. MySQL dibaca MY-ES-KYOO-EL [maɪˌɛsˌkjuːˈɛl].</p>
<h2 id="sejarah-mysql">SEJARAH MYSQL</h2>
<p><img src="https://images.pexels.com/photos/1181316/pexels-photo-1181316.jpeg?auto=compress&amp;cs=tinysrgb&amp;dpr=2&amp;w=500" alt=""><br>
<small>image courtesy : <a href="https://www.pexels.com/@divinetechygirl">https://www.pexels.com/@divinetechygirl</a></small></p>
<p>Beberapa orang bahkan membaca MySQL seperti sedang menyebutkan “my sequel”. MySQL AB, sebuah perusahaan asal Swedia, menjadi yang pertama dalam mengembangkan MySQL di tahun 1994. Hak kepemilikan MySQL kemudian diambil secara menyeluruh oleh perusahaan teknologi Amerika Serikat, Sun Microsystems, ketika mereka membeli MySQL AB pada tahun 2008. Di tahun 2010, Oracle yang adalah salah satu perusahaan teknologi terbesar di Amerika Serikat mengakuisisi Sun Microsystems. Semenjak itulah, MySQL sepenuhnya dimiliki oleh Oracle.</p>
<h2 id="instalasi">Instalasi</h2>
<p>Untuk menggunakan MYSQL pada localhost komputer kita, dibutuhkan sebuah software bernama <strong>MAMP</strong> / <strong>LAMPP</strong>/<strong>XAMPP</strong>.</p>
<p>Bagi pengguna windows, sangat familiar penggunaan XAMPP, Huruf <strong>M</strong>, adalah singkatan Macos, dan <strong>L</strong> adalah Linux, dan <strong>X</strong> adalah multi platform alias X-ross Platform.</p>
<p><img src="https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6xkzlgl8odo6wd9spg75.png" alt="Alt Text"><br>
<small>uploaded in <a href="https://dev.to">https://dev.to</a></small></p>
<p>Okay di JVALLEY kita akan sama sama menggunakan sebuah software bernama XAMPP silakan install di <a href="https://www.apachefriends.org/index.html">Link Berikut</a></p>
<p>Silakan install seperti biasa, dan jalankan servernya…</p>
<p>Setelah server berjalan, teman teman akan di munculkan sebuah halaman web milik apache web server.</p>
<blockquote>
<p>Pastikan XAMPP Server sudah berjalan dan di centang mysql dan apachenya</p>
</blockquote>
<h2 id="php-my-admin">PHP MY ADMIN</h2>
<p>Php My Admin merupakan sebuah web base server dashboard untuk pengaturan database kita. Semua proses pembuatan database, dan edit edit bisa di lakukan disini.</p>
<p>Silakan akses php myadmin dengan cara mengetikan <a href="http://localhost/phpmyadmin">http://localhost/phpmyadmin</a> pada browser teman teaman.</p>
<blockquote>
<p>Periksa port yang berjalan di system apache teman teamn.<br>
Untuk yang port apachenya berbeda, silakan teambahkan titik2 ( : ) dan portnya setelah localhost, misal <a href="http://localhost:8888/phpmyadmin">http://localhost:8888/phpmyadmin</a></p>
</blockquote>
<p><img src="https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ab6nmnn4t6aotri6cy5p.png" alt="Alt Text"><br>
<small>uploaded in <a href="https://dev.to">https://dev.to</a></small></p>
<blockquote>
<p>Meski tampilannya agak jadul, tapi PHP My admin adalah web base dasboard paling popular bagi pengguna database MYSQL hingga saat ini.</p>
</blockquote>
<h3 id="mebuat-database-baru-dengan-php-my-admin">Mebuat database baru dengan php my admin</h3>
<p>Okay sekarang kita akan membuat sebuah database baru dengan nama <strong>jvalleymember</strong>.</p>
<p><img src="https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qtc0fms2ouo3f7wr8h9a.png" alt="Alt Text"></p>
<p>Silakan click Text <strong>New</strong> di panel sebelah kiri layar,<br>
dan pada panel tengah silakan isikan form database name dengan <strong>jvalleymember</strong></p>
<p><img src="https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zhwrnuebw27opzyg39jq.png" alt="Alt Text"></p>
<p>Langsung saja click create dan jvalley member database sudah berhasil dibuat, silakan check panel sebelah kiri kembali dan lihat sudah muncul jvalleymeber.</p>
<h3 id="membuat-table-pada-database">Membuat Table pada database</h3>
<p>Silakan click di panel sebelah kiri, dan pilih <em>jvalleymember</em> panel kanan akan berubah ke create table panel, ketikan nama <strong>users</strong> pada kolom new table. dan pada <em>Number of Column</em> silakan masukan angka 5.<br>
<img src="https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9u13yzx2kbfgiimukhb4.png" alt="Alt Text"></p>
<p>Langsung saja create dengan menekan tombol <em>go</em> yang ada di sebelah ujung kanan.</p>
<p>Atur table pertama dengan type data <em>INT</em> value kosongkan dan atur ID ini sebagai <em>Primary Key</em><br>
<img src="https://dev-to-uploads.s3.amazonaws.com/uploads/articles/46xasl1e1khspoyq48z5.png" alt="Alt Text"></p>
<p>Sisanya silakan ikuti gambar dibawah ini :<br>
<img src="https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jhf6eljdbrgr4cwayv0w.png" alt="Alt Text"></p>
<p>Dan silakan tekan <strong>SAVE</strong>, dan table users akan berhasil di tambahkan ke database <em>jvalleymember</em></p>
<h2 id="access-mysql-via-cli">Access MYSQL via CLI</h2>
<p>Silakan buka terminal dan ketikan</p>
<pre><code>mysql -u root -p
</code></pre>
<p>Ketika ditanyakan password silakan kosongkan dan tekan <strong>ENTER</strong></p>
<p>cursor akan berubah menjadi <code>mysql&gt;</code><br>
tandanya teman teman sudah berhasil masuk ke dalam MYSQL CLI.</p>
<h3 id="melihat-seluruh-data-yang-ada-di-mysql">Melihat seluruh data yang ada di MYSQL</h3>
<p>Untuk melihat semua database yang tersedia di MYSQL kita, silakan teman teman ketik :<br>
<code>SHOW DATABASES;</code></p>
<blockquote>
<p>Titik koma pada akhir statent sifatnya wajib<br>
akan tetapi penggunaan Capital tidak wajib</p>
</blockquote>
<p><img src="https://dev-to-uploads.s3.amazonaws.com/uploads/articles/l4cn5dzdwh5lk9541h96.png" alt="Alt Text"></p>
<p>Teman teman bisa lihat, database yang sebelumnya kita buat di php my admin sudah ada juga disini.</p>
<h3 id="menambahkan-database-ke-dalam-table-users">Menambahkan database ke dalam table users</h3>
<p>Sekarang kita coba untuk menambahkan satu data ke dalam table <strong>users</strong> yang ada di database jvalleymember.</p>
<p>Silakan ketikan syntax berikut</p>
<pre class=" language-mysql"><code class="prism  language-mysql">insert into jvalleymember.users(email, username, password, phone) values("fadliselaz@gmail.com", "fadliselaz", "12341234", "081214123123");
</code></pre>
<blockquote>
<p>Silakan masukan data setelah values( dengan data teman teamn sendiri…<br>
<img src="https://dev-to-uploads.s3.amazonaws.com/uploads/articles/myilm865i38rpb6bceoc.png" alt="Alt Text"></p>
</blockquote>
<p>Jika muncul gambar seperti di atas, artinya teman teman berhasil menambah satu data ke dalam table users. Silakan tambahkan beberapa data lainnya.</p>
<h2 id="show-table-user">Show table user</h2>
<p>untuk melihat semua data yang ada di table users silakan ketik</p>
<pre><code>select * from jvalleymember.users;
</code></pre>
<p><img src="https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oly027xnfnadc33n9cud.png" alt="Alt Text"></p>
<h2 id="update-data-pada-tabel-users">Update data pada tabel users</h2>
<p>Kita akan mengedit username pada row dengan id 1 dengan cara :</p>
<pre><code>UPDATE jvalleymember.users SET username="evalia" WHERE id=1;
</code></pre>
<h2 id="delete-data-dari-table-users">Delete Data dari table users</h2>
<p>Untuk mendelete data pada table, silakan dengan cara :</p>
<pre><code>DELETE FROM jvalleymember.users WHERE id=1;
</code></pre>
<p>Okay, sampai disini dulu ya gengs… <em>Good Luck</em></p>

