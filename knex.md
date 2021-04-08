---


---

<h1 id="express-menggunakan-query-builder-bernama-knex">Express menggunakan Query Builder bernama KNEX</h1>
<p><img src="https://images.pexels.com/photos/4497195/pexels-photo-4497195.jpeg?auto=compress&amp;cs=tinysrgb&amp;dpr=2&amp;w=500" alt="pexels image"><br>
Apa itu query builder, mugkin teman teman familiar dengan query MYSQL yang seperti ini :</p>
<pre class=" language-bash"><code class="prism  language-bash">SELECT * FROM <span class="token function">users</span> WHERE id<span class="token operator">=</span>1<span class="token punctuation">;</span>
</code></pre>
<p>Ya, syntax diatas merupakan sebuah query language pada DBMS MYSQL. nah untuk di express, kita bisa mempermudah query language tersebut dengan bantuan <strong>query builder</strong> bernama <em>KNEX</em>.</p>
<p>Knex memungkinkan kita mengunakan query language bawaan pada MYSQL dengan lebih ringkas.<br>
Silakan teman teman buat sebuah project nodejs dan install beberapa package seperti dibawah ini :</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> <span class="token function">install</span> --save express express-handlebars cors knex
</code></pre>
<p>Buat sebuah file bernama <strong>server.js</strong> dan buat sebuah skema express seperti yang sudah teman teman pelajari.</p>
<ul>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Ubah package.json bagian test menjadi dev</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Pada file server.js import semua kebutuhan project</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Buat Middleware</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Set Template Engine</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Buat Routing</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Buat Listener</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Buat Folder Public, Views, Controller dan Model</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> isi public dengan kebutuhan static seperti css dan javascript client</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> isi views dengan kebutuhan template engine kita</li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> isi folder controller dengan file bernama <em>homeController.js</em></li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> isi folder Model dengan file bernama <em>AbsenSiswaModel.js</em> dan <em>connection.js</em></li>
<li class="task-list-item"><input type="checkbox" class="task-list-item-checkbox" disabled=""> Pada <em>server.js</em> silakan isi dengan default configuration yang sudah kita pelajari</li>
</ul>
<p>Buat sekumpulan statment untuk import package ke dalam applikasi kita<br>
<small>server.js</small></p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> express <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"express"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> cors <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"cors"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> hbs <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"express-handlebars"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> path <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"path"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> app <span class="token operator">=</span> <span class="token function">express</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span>  home  <span class="token operator">=</span>  <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"./controllers/homeControllers"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>Buat sekumpulan statment untuk middleware<br>
<small>server.js</small></p>
<pre class=" language-javascript"><code class="prism  language-javascript">app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span><span class="token function">cors</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span>express<span class="token punctuation">.</span><span class="token function">urlencoded</span><span class="token punctuation">(</span><span class="token punctuation">{</span> extended<span class="token punctuation">:</span> <span class="token boolean">false</span> <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span>express<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span>express<span class="token punctuation">.</span><span class="token keyword">static</span><span class="token punctuation">(</span>path<span class="token punctuation">.</span><span class="token function">join</span><span class="token punctuation">(</span>__dirname<span class="token punctuation">,</span> <span class="token string">"public"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>Buat sekumpulan statment untuk setup view engine<br>
<small>server.js</small></p>
<pre class=" language-javascript"><code class="prism  language-javascript">app<span class="token punctuation">.</span><span class="token keyword">set</span><span class="token punctuation">(</span><span class="token string">"views"</span><span class="token punctuation">,</span> path<span class="token punctuation">.</span><span class="token function">join</span><span class="token punctuation">(</span>__dirname<span class="token punctuation">,</span> <span class="token string">"views"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token keyword">set</span><span class="token punctuation">(</span><span class="token string">"view engine"</span><span class="token punctuation">,</span> <span class="token string">"html"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token function">engine</span><span class="token punctuation">(</span><span class="token string">"html"</span><span class="token punctuation">,</span> <span class="token function">hbs</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
    layoutsDir<span class="token punctuation">:</span> path<span class="token punctuation">.</span><span class="token function">join</span><span class="token punctuation">(</span>__dirname<span class="token punctuation">,</span> <span class="token string">"views/layouts"</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
    partialsDir<span class="token punctuation">:</span> path<span class="token punctuation">.</span><span class="token function">join</span><span class="token punctuation">(</span>__dirname<span class="token punctuation">,</span> <span class="token string">"views/components"</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
    defaultLayout<span class="token punctuation">:</span> <span class="token string">"main_layout.html"</span><span class="token punctuation">,</span>
    extname<span class="token punctuation">:</span> <span class="token string">"html"</span><span class="token punctuation">,</span>
  <span class="token punctuation">}</span><span class="token punctuation">)</span>
<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>Buat sekumpulan statment untuk Routing<br>
<small>server.js</small></p>
<pre class=" language-javascript"><code class="prism  language-javascript">app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span><span class="token string">"/"</span><span class="token punctuation">,</span> home<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>Buat sekumpulan statment untuk Listener<br>
<small>server.js</small></p>
<pre class=" language-javascript"><code class="prism  language-javascript">app<span class="token punctuation">.</span><span class="token function">listen</span><span class="token punctuation">(</span><span class="token number">3000</span><span class="token punctuation">,</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span>  console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">"listen port 3000"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h1 id="model">Model</h1>
<p><img src="https://images.pexels.com/photos/3683056/pexels-photo-3683056.jpeg?auto=compress&amp;cs=tinysrgb&amp;dpr=2&amp;w=500" alt=""><br>
Model merupakan sekumpulan function untuk menghubungkan logic dengan database, untuk koneksi ke database kita menggunakan sebuah query builder bernama <strong>knex</strong>.</p>
<p>Buat sebuah folder bernama model, dan buat 2 buah file bernama <em>AbsenSiswaModel.js</em> dan <em>connection.js</em>.<br>
File <strong>connection.js</strong> akan berisi statment untuk mengkoneksikan project kita ini dengna database.</p>
<p><small>/model/connection.js</small></p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> db <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"knex"</span><span class="token punctuation">)</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
  client<span class="token punctuation">:</span> <span class="token string">"mysql"</span><span class="token punctuation">,</span>
  connection<span class="token punctuation">:</span> <span class="token punctuation">{</span>
    host<span class="token punctuation">:</span> <span class="token string">"127.0.0.1"</span><span class="token punctuation">,</span>
    user<span class="token punctuation">:</span> <span class="token string">"root"</span><span class="token punctuation">,</span>
    password<span class="token punctuation">:</span> <span class="token string">"root"</span><span class="token punctuation">,</span>
    database<span class="token punctuation">:</span> <span class="token string">"absenSiswa"</span><span class="token punctuation">,</span>
    port<span class="token punctuation">:</span> <span class="token number">3306</span><span class="token punctuation">,</span>
  <span class="token punctuation">}</span><span class="token punctuation">,</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

module<span class="token punctuation">.</span>exports <span class="token operator">=</span> db<span class="token punctuation">;</span>
</code></pre>
<p>Silakan buka file <strong>AbsenSiswaModel.js</strong> dan isi dengan code berikut :<br>
<small>/model/AbsenSiswaModel.js</small></p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token comment">//import connection</span>
<span class="token keyword">const</span> db <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"./connection"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">//mendapatkan semua data siswa</span>
<span class="token keyword">const</span> getAllSiswa <span class="token operator">=</span> <span class="token keyword">async</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
  <span class="token keyword">return</span> <span class="token keyword">await</span> db
    <span class="token punctuation">.</span><span class="token keyword">from</span><span class="token punctuation">(</span><span class="token string">"siswa"</span><span class="token punctuation">)</span>
    <span class="token punctuation">.</span><span class="token function">select</span><span class="token punctuation">(</span><span class="token string">"*"</span><span class="token punctuation">)</span>
    <span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span><span class="token punctuation">(</span>rows<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
      <span class="token keyword">return</span> rows<span class="token punctuation">;</span>
    <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>

<span class="token comment">//export semua function</span>
module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token punctuation">{</span> getAllSiswa <span class="token punctuation">}</span><span class="token punctuation">;</span>
</code></pre>
<h1 id="controller">Controller</h1>
<p><img src="https://images.pexels.com/photos/892543/pexels-photo-892543.jpeg?auto=compress&amp;cs=tinysrgb&amp;dpr=2&amp;w=500" alt=""><br>
Pada sebuah project MVC, fungsi controller adalah untuk menghubungkan jalur jalur data, yang bisa di tampilkan ke client.<br>
Silakan teman teman ke sebuah folder yang sudah kita buat bernama controller, dan buat sebuah file bernama <em>homeController.js</em>.</p>
<p>Import package yang kita butuhkan :<br>
<small>/controller/homeController.js</small></p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> express <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"express"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> home <span class="token operator">=</span> express<span class="token punctuation">.</span><span class="token function">Router</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> <span class="token punctuation">{</span> getAllSiswa <span class="token punctuation">}</span> <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"../model/AbsenSiswaModel"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>Buat sebuah function untuk menangani controller ke sebuah url “/”<br>
<small>/controller/homeController.js</small></p>
<pre class=" language-javascript"><code class="prism  language-javascript">home<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">"/"</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
  <span class="token function">getAllSiswa</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span><span class="token punctuation">(</span>result<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
    res<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span>result<span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h1 id="view">View</h1>
<p><img src="https://images.pexels.com/photos/1323550/pexels-photo-1323550.jpeg?auto=compress&amp;cs=tinysrgb&amp;dpr=2&amp;w=500" alt=""><br>
Oke kita akan buat tampilan pada browser pada folder view, silakan buat 2 buah folder lagi di dalam folder views bernama <strong>components</strong> dan <strong>layouts</strong>. jangan lupa buat file bernama <strong>home.html</strong> pada default directory views.</p>
<p>Pertama kita harus membuat sebuah default layouts, buat sebuah file bernama <strong>main_layout.html</strong> didalam sebuah folder bernama <em>layouts</em>. Silakan isi dengan html sebagai berikut.</p>
<pre class=" language-html"><code class="prism  language-html"><span class="token doctype">&lt;!DOCTYPE html&gt;</span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>html</span> <span class="token attr-name">lang</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>en<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>head</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>meta</span> <span class="token attr-name">charset</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>UTF-8<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>meta</span> <span class="token attr-name">http-equiv</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>X-UA-Compatible<span class="token punctuation">"</span></span> <span class="token attr-name">content</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>IE=edge<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>meta</span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>viewport<span class="token punctuation">"</span></span> <span class="token attr-name">content</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>width=device-width, initial-scale=1.0<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>link</span> <span class="token attr-name">rel</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>stylesheet<span class="token punctuation">"</span></span> <span class="token attr-name">href</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>style.css<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>title</span><span class="token punctuation">&gt;</span></span>Express Mysql<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>title</span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>head</span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>body</span><span class="token punctuation">&gt;</span></span>
    {{{ body }}}
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>script</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>main.js<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span><span class="token script language-javascript"></span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>script</span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>body</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>html</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>dan silakan buka file bernama <strong>home.html</strong> pada default directory views, dan masukan code berikut:</p>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>main</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>container-fluid flex-center<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>h1</span><span class="token punctuation">&gt;</span></span>Welcome home<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>h1</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>main</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<h2 id="menampilkan-hasil-fetch-database-ke-view">Menampilkan Hasil fetch database ke View</h2>
<p>Okay teman teman, sekarang kita akan tampilkan data dari database ke view.</p>
<p>Silakan ke file <em>/controller/homeController.js</em> dan ubah routing seperti di bawah ini :</p>
<pre class=" language-javascript"><code class="prism  language-javascript">home<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">"/"</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
  <span class="token function">getAllSiswa</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span><span class="token punctuation">(</span>result<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
    res<span class="token punctuation">.</span><span class="token function">render</span><span class="token punctuation">(</span><span class="token string">"home"</span><span class="token punctuation">,</span> <span class="token punctuation">{</span> data<span class="token punctuation">:</span> result <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>Perhatikan code di atas, kita merender ke sebuah file html berikut mengirimkan data dengan variable result sebagai aliasnya.</p>
<p>Sekarang silakan teman teman buka file view dan buat seperti di bawah ini :</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token operator">&lt;</span>main <span class="token keyword">class</span><span class="token operator">=</span><span class="token string">"container-fluid flex-center"</span><span class="token operator">&gt;</span>
  <span class="token operator">&lt;</span>table <span class="token keyword">class</span><span class="token operator">=</span><span class="token string">"siswa_list"</span><span class="token operator">&gt;</span>
      <span class="token operator">&lt;</span>thead<span class="token operator">&gt;</span>
          <span class="token operator">&lt;</span>tr<span class="token operator">&gt;</span>
              <span class="token operator">&lt;</span>td<span class="token operator">&gt;</span>ID<span class="token operator">&lt;</span><span class="token operator">/</span>td<span class="token operator">&gt;</span>
              <span class="token operator">&lt;</span>td<span class="token operator">&gt;</span>NAMA<span class="token operator">&lt;</span><span class="token operator">/</span>td<span class="token operator">&gt;</span>
              <span class="token operator">&lt;</span>td<span class="token operator">&gt;</span>EMAIL<span class="token operator">&lt;</span><span class="token operator">/</span>td<span class="token operator">&gt;</span>
              <span class="token operator">&lt;</span>td<span class="token operator">&gt;</span>PHONE<span class="token operator">&lt;</span><span class="token operator">/</span>td<span class="token operator">&gt;</span>
              <span class="token operator">&lt;</span>td<span class="token operator">&gt;</span>BATCH<span class="token operator">&lt;</span><span class="token operator">/</span>td<span class="token operator">&gt;</span>
              <span class="token operator">&lt;</span>td<span class="token operator">&gt;</span>DATE<span class="token operator">&lt;</span><span class="token operator">/</span>td<span class="token operator">&gt;</span>
          <span class="token operator">&lt;</span><span class="token operator">/</span>tr<span class="token operator">&gt;</span>
        <span class="token operator">&lt;</span><span class="token operator">/</span>thead<span class="token operator">&gt;</span>
        <span class="token operator">&lt;</span>tbody<span class="token operator">&gt;</span>
            <span class="token punctuation">{</span><span class="token punctuation">{</span>#each data<span class="token punctuation">}</span><span class="token punctuation">}</span> 
                <span class="token operator">&lt;</span>tr<span class="token operator">&gt;</span>
                    <span class="token operator">&lt;</span>td<span class="token operator">&gt;</span><span class="token punctuation">{</span><span class="token punctuation">{</span><span class="token keyword">this</span><span class="token punctuation">.</span>id<span class="token punctuation">}</span><span class="token punctuation">}</span><span class="token operator">&lt;</span><span class="token operator">/</span>td<span class="token operator">&gt;</span>
                    <span class="token operator">&lt;</span>td<span class="token operator">&gt;</span><span class="token punctuation">{</span><span class="token punctuation">{</span><span class="token keyword">this</span><span class="token punctuation">.</span>nama<span class="token punctuation">}</span><span class="token punctuation">}</span><span class="token operator">&lt;</span><span class="token operator">/</span>td<span class="token operator">&gt;</span>
                    <span class="token operator">&lt;</span>td<span class="token operator">&gt;</span><span class="token punctuation">{</span><span class="token punctuation">{</span><span class="token keyword">this</span><span class="token punctuation">.</span>email<span class="token punctuation">}</span><span class="token punctuation">}</span><span class="token operator">&lt;</span><span class="token operator">/</span>td<span class="token operator">&gt;</span>
                    <span class="token operator">&lt;</span>td<span class="token operator">&gt;</span><span class="token punctuation">{</span><span class="token punctuation">{</span><span class="token keyword">this</span><span class="token punctuation">.</span>telpon<span class="token punctuation">}</span><span class="token punctuation">}</span><span class="token operator">&lt;</span><span class="token operator">/</span>td<span class="token operator">&gt;</span>
                    <span class="token operator">&lt;</span>td<span class="token operator">&gt;</span><span class="token punctuation">{</span><span class="token punctuation">{</span><span class="token keyword">this</span><span class="token punctuation">.</span>batch<span class="token punctuation">}</span><span class="token punctuation">}</span><span class="token operator">&lt;</span><span class="token operator">/</span>td<span class="token operator">&gt;</span>
                    <span class="token operator">&lt;</span>td name<span class="token operator">=</span><span class="token string">"{{this.date}}"</span> <span class="token keyword">class</span><span class="token operator">=</span><span class="token string">"date"</span> id<span class="token operator">=</span><span class="token string">"{{this.id}}"</span><span class="token operator">&gt;</span><span class="token punctuation">{</span><span class="token punctuation">{</span><span class="token keyword">this</span><span class="token punctuation">.</span>date<span class="token punctuation">}</span><span class="token punctuation">}</span><span class="token operator">&lt;</span><span class="token operator">/</span>td<span class="token operator">&gt;</span>
                    <span class="token operator">&lt;</span>input type<span class="token operator">=</span><span class="token string">"hidden"</span> <span class="token keyword">class</span><span class="token operator">=</span><span class="token string">"res_date{{this.id}}"</span> value<span class="token operator">=</span><span class="token string">"{{this.date}}"</span><span class="token operator">&gt;</span>
                <span class="token operator">&lt;</span><span class="token operator">/</span>tr<span class="token operator">&gt;</span>
            <span class="token punctuation">{</span><span class="token punctuation">{</span><span class="token operator">/</span>each<span class="token punctuation">}</span><span class="token punctuation">}</span>
        <span class="token operator">&lt;</span><span class="token operator">/</span>tbody<span class="token operator">&gt;</span>
  <span class="token operator">&lt;</span><span class="token operator">/</span>ul<span class="token operator">&gt;</span>
<span class="token operator">&lt;</span><span class="token operator">/</span>main<span class="token operator">&gt;</span>
</code></pre>

