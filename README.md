# Express menggunakan Query Builder bernama KNEX

![pexels image](https://images.pexels.com/photos/4497195/pexels-photo-4497195.jpeg?auto=compress&cs=tinysrgb&dpr=2&w=500)
Apa itu query builder, mugkin teman teman familiar dengan query MYSQL yang seperti ini :

```bash
SELECT * FROM users WHERE id=1;
```

Ya, syntax diatas merupakan sebuah query language pada DBMS MYSQL. nah untuk di express, kita bisa mempermudah query language tersebut dengan bantuan **query builder** bernama _KNEX_.

Knex memungkinkan kita mengunakan query language bawaan pada MYSQL dengan lebih ringkas.
Silakan teman teman buat sebuah project nodejs dan install beberapa package seperti dibawah ini :

```bash
npm install --save express express-handlebars cors knex
```

Buat sebuah file bernama **server.js** dan buat sebuah skema express seperti yang sudah teman teman pelajari.

- [ ] Ubah package.json bagian test menjadi dev
- [ ] Pada file server.js import semua kebutuhan project
- [ ] Buat Middleware
- [ ] Set Template Engine
- [ ] Buat Routing
- [ ] Buat Listener
- [ ] Buat Folder Public, Views, Controller dan Model
- [ ] isi public dengan kebutuhan static seperti css dan javascript client
- [ ] isi views dengan kebutuhan template engine kita
- [ ] isi folder controller dengan file bernama _homeController.js_
- [ ] isi folder Model dengan file bernama _AbsenSiswaModel.js_ dan _connection.js_
- [ ] Pada _server.js_ silakan isi dengan default configuration yang sudah kita pelajari

Buat sekumpulan statment untuk import package ke dalam applikasi kita
<small>server.js</small>

```javascript
const express = require("express");
const cors = require("cors");
const hbs = require("express-handlebars");
const path = require("path");
const app = express();
const home = require("./controllers/homeControllers");
```

Buat sekumpulan statment untuk middleware
<small>server.js</small>

```javascript
app.use(cors());
app.use(express.urlencoded({ extended: false }));
app.use(express.json());
app.use(express.static(path.join(__dirname, "public")));
```

Buat sekumpulan statment untuk setup view engine
<small>server.js</small>

```javascript
app.set("views", path.join(__dirname, "views"));
app.set("view engine", "html");
app.engine(
  "html",
  hbs({
    layoutsDir: path.join(__dirname, "views/layouts"),
    partialsDir: path.join(__dirname, "views/components"),
    defaultLayout: "main_layout.html",
    extname: "html",
  })
);
```

Buat sekumpulan statment untuk Routing
<small>server.js</small>

```javascript
app.use("/", home);
```

Buat sekumpulan statment untuk Listener
<small>server.js</small>

```javascript
app.listen(3000, () => console.log("listen port 3000"));
```

# Model

![](https://images.pexels.com/photos/3683056/pexels-photo-3683056.jpeg?auto=compress&cs=tinysrgb&dpr=2&w=500)
Model merupakan sekumpulan function untuk menghubungkan logic dengan database, untuk koneksi ke database kita menggunakan sebuah query builder bernama **knex**.

Buat sebuah folder bernama model, dan buat 2 buah file bernama _AbsenSiswaModel.js_ dan _connection.js_.
File **connection.js** akan berisi statment untuk mengkoneksikan project kita ini dengna database.

<small>/model/connection.js</small>

```javascript
const db = require("knex")({
  client: "mysql",
  connection: {
    host: "127.0.0.1",
    user: "root",
    password: "root",
    database: "absenSiswa",
    port: 3306,
  },
});

module.exports = db;
```

Silakan buka file **AbsenSiswaModel.js** dan isi dengan code berikut :
<small>/model/AbsenSiswaModel.js</small>

```javascript
//import connection
const db = require("./connection");

//mendapatkan semua data siswa
const getAllSiswa = async () => {
  return await db
    .from("siswa")
    .select("*")
    .then((rows) => {
      return rows;
    });
};

//export semua function
module.exports = { getAllSiswa };
```

# Controller

![](https://images.pexels.com/photos/892543/pexels-photo-892543.jpeg?auto=compress&cs=tinysrgb&dpr=2&w=500)
Pada sebuah project MVC, fungsi controller adalah untuk menghubungkan jalur jalur data, yang bisa di tampilkan ke client.
Silakan teman teman ke sebuah folder yang sudah kita buat bernama controller, dan buat sebuah file bernama _homeController.js_.

Import package yang kita butuhkan :
<small>/controller/homeController.js</small>

```javascript
const express = require("express");
const home = express.Router();
const { getAllSiswa } = require("../model/AbsenSiswaModel");
```

Buat sebuah function untuk menangani controller ke sebuah url "/"
<small>/controller/homeController.js</small>

```javascript
home.get("/", (req, res) => {
  getAllSiswa().then((result) => {
    res.json(result);
  });
});
```

# View

![](https://images.pexels.com/photos/1323550/pexels-photo-1323550.jpeg?auto=compress&cs=tinysrgb&dpr=2&w=500)
Oke kita akan buat tampilan pada browser pada folder view, silakan buat 2 buah folder lagi di dalam folder views bernama **components** dan **layouts**. jangan lupa buat file bernama **home.html** pada default directory views.

Pertama kita harus membuat sebuah default layouts, buat sebuah file bernama **main_layout.html** didalam sebuah folder bernama _layouts_. Silakan isi dengan html sebagai berikut.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>Express Mysql</title>
  </head>
  <body>
    {{{ body }}}
    <script src="main.js"></script>
  </body>
</html>
```

dan silakan buka file bernama **home.html** pada default directory views, dan masukan code berikut:

```html
<main class="container-fluid flex-center">
  <h1>Welcome home</h1>
</main>
```

## Menampilkan Hasil fetch database ke View

Okay teman teman, sekarang kita akan tampilkan data dari database ke view.

Silakan ke file _/controller/homeController.js_ dan ubah routing seperti di bawah ini :

```javascript
home.get("/", (req, res) => {
  getAllSiswa().then((result) => {
    res.render("home", { data: result });
  });
});
```

Perhatikan code di atas, kita merender ke sebuah file html berikut mengirimkan data dengan variable result sebagai aliasnya.

Sekarang silakan teman teman buka file view dan buat seperti di bawah ini :

```javascript
<main class="container-fluid flex-center">
  <table class="siswa_list">
      <thead>
          <tr>
              <td>ID</td>
              <td>NAMA</td>
              <td>EMAIL</td>
              <td>PHONE</td>
              <td>BATCH</td>
              <td>DATE</td>
          </tr>
        </thead>
        <tbody>
            {{#each data}}
                <tr>
                    <td>{{this.id}}</td>
                    <td>{{this.nama}}</td>
                    <td>{{this.email}}</td>
                    <td>{{this.telpon}}</td>
                    <td>{{this.batch}}</td>
                    <td name="{{this.date}}" class="date" id="{{this.id}}">{{this.date}}</td>
                    <input type="hidden" class="res_date{{this.id}}" value="{{this.date}}">
                </tr>
            {{/each}}
        </tbody>
  </ul>
</main>
```

# Menbuat form absen dan memasukan data ke database

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/z68fxb5pdim5pl453p8v.png)

Silakan teman teman buka folder /views/components dan buat sebuah component baru bernama **formAbsen.html**

<small>/views/components/formAbsen.html</small>

```html
<form action="/absen" class="form_absen" method="POST">
  <div class="form_group">
    <label for="nama">nama</label>
    <input type="text" id="nama" name="nama" required />
  </div>

  <div class="form_group">
    <label for="email">email</label>
    <input type="email" id="email" name="email" required />
  </div>

  <div class="form_group">
    <label for="telpon">telpon</label>
    <input type="phone" id="telpon" name="telpon" required />
  </div>

  <div class="form_group">
    <label for="batch">batch</label>
    <input type="number" id="batch" name="batch" required />
  </div>

  <button type="submit">absen</button>
</form>
```

Kita buat sebuah form untuk mengisi data ke database.

> Jangan lupa untuk memberikan sebuah property method="POST", karena kita akan melakukan post ke database

Selanjutnya silakan teman teman ke sebuah file bernama **absenSiswaModel.js**
dan tambahkan sebuah statment model seperti dibawah ini :

```javascript
//menambahkan absen
const storeAbsen = async (data) => {
  return await db
    .from("siswa")
    .insert({
      nama: data.nama,
      email: data.email,
      telpon: data.telpon,
      batch: data.batch,
    })
    .then((rows) => {
      return rows;
    })
    .catch((err) => console.log(err));
};
```

Perhatikan code di atas, kita telah membuah sebuah function _ASYNCRONUS_ bernama **storeAbsen**, yang di dalamnya mengembalikan sebuah function connection ke database menggunakan knex _INSERT_.

Selanjutnya jangan lupa export function tersebut agar bisa di gunakan di file controller.

```javascript
//export semua function
module.exports = { getAllSiswa, storeAbsen };
```

Okay, saatnya kita mengatur controller untuk menambahkan data ini, silakan teman teman buka sebuah file **/controller/homeController.js** dan tambah kan sebuah route baru :

```javascript
home.post("/absen", (req, res) => {
  let nama = req.body.nama;
  let email = req.body.email;
  let telpon = req.body.telpon;
  let batch = req.body.batch;

  storeAbsen({
    nama: nama,
    email: email,
    telpon: telpon,
    batch: batch,
  }).then((result) => {
    res.redirect("/");
  });
});
```

> Bisa dilihat di code diatas bahwa kita menggunakan home.post bukan get, karena form data yang kita kirimkan mempunyai method POST

Selanjutnya kita tinggal tambahkan partial file atau component pada file **/views/home.html** seperti contoh di bawah ini.

```html
{{> formAbsen}}
```

letakan dimanapun karena kita akan atur cssnya menjadi fixed.

Terakhir kita bisa menambahkan css ke file **public/style.css** :

```css
.form_absen {
  width: 250px;
  height: auto;
  padding: 20px;
  background-color: whitesmoke;
  border: 0.5px solid gray;
  display: flex;
  flex-direction: column;
  gap: 20px;
  position: fixed;
  bottom: 20px;
  left: 20px;
}

.form_group {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
```
