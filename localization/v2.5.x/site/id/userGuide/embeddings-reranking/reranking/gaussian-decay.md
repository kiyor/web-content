---
id: gaussian-decay.md
title: Peluruhan GaussianCompatible with Milvus 2.6.x
summary: >-
  Peluruhan Gaussian, juga dikenal sebagai peluruhan normal, menciptakan
  penyesuaian yang terasa paling alami pada hasil pencarian Anda. Seperti
  penglihatan manusia yang secara bertahap mengabur seiring dengan jarak,
  peluruhan Gaussian menciptakan kurva berbentuk lonceng yang secara perlahan
  mengurangi relevansi saat item menjauh dari titik ideal Anda. Pendekatan ini
  sangat ideal ketika Anda menginginkan peluruhan yang seimbang yang tidak
  menghukum item yang berada di luar rentang yang Anda inginkan, tetapi masih
  secara signifikan mengurangi relevansi item yang jauh.
beta: Milvus 2.6.x
---
<h1 id="Gaussian-Decay" class="common-anchor-header">Peluruhan Gaussian<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Gaussian-Decay" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h1><p>Peluruhan Gaussian, juga dikenal sebagai peluruhan normal, menciptakan penyesuaian yang terasa paling alami pada hasil pencarian Anda. Seperti penglihatan manusia yang secara bertahap mengabur seiring jarak, peluruhan Gaussian menciptakan kurva berbentuk lonceng yang secara perlahan mengurangi relevansi saat item menjauh dari titik ideal Anda. Pendekatan ini sangat ideal jika Anda menginginkan peluruhan yang seimbang yang tidak menghukum item yang berada di luar kisaran yang Anda inginkan, tetapi masih secara signifikan mengurangi relevansi item yang jauh.</p>
<p>Tidak seperti pemeringkat peluruhan lainnya:</p>
<ul>
<li><p>Peluruhan eksponensial turun tajam pada awalnya, menciptakan penalti awal yang lebih kuat</p></li>
<li><p>Peluruhan linier menurun dengan kecepatan konstan hingga mencapai nol, menciptakan batas yang jelas</p></li>
</ul>
<p>Peluruhan Gaussian memberikan pendekatan yang lebih seimbang dan intuitif yang terasa alami bagi pengguna.</p>
<h2 id="When-to-use-Gaussian-decay" class="common-anchor-header">Kapan menggunakan peluruhan Gaussian<button data-href="#When-to-use-Gaussian-decay" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>Peluruhan Gaussian sangat efektif untuk:</p>
<table>
   <tr>
     <th><p>Kasus Penggunaan</p></th>
     <th><p>Contoh</p></th>
     <th><p>Mengapa Gaussian Bekerja dengan Baik</p></th>
   </tr>
   <tr>
     <td><p>Pencarian berbasis lokasi</p></td>
     <td><p>Pencari restoran, pencari lokasi toko</p></td>
     <td><p>Meniru persepsi alami manusia tentang relevansi jarak</p></td>
   </tr>
   <tr>
     <td><p>Rekomendasi konten</p></td>
     <td><p>Saran artikel berdasarkan tanggal publikasi</p></td>
     <td><p>Penurunan relevansi secara bertahap seiring bertambahnya usia konten</p></td>
   </tr>
   <tr>
     <td><p>Daftar produk</p></td>
     <td><p>Item dengan harga mendekati target</p></td>
     <td><p>Penurunan relevansi yang mulus saat harga menyimpang dari target</p></td>
   </tr>
   <tr>
     <td><p>Pencocokan keahlian</p></td>
     <td><p>Menemukan profesional dengan pengalaman yang relevan</p></td>
     <td><p>Penilaian relevansi pengalaman yang seimbang</p></td>
   </tr>
</table>
<p>Jika aplikasi Anda memerlukan perasaan alami penurunan relevansi tanpa hukuman yang keras atau batas waktu yang ketat, peluruhan Gaussian mungkin merupakan pilihan terbaik Anda.</p>
<h2 id="Bell-curve-principle" class="common-anchor-header">Prinsip kurva lonceng<button data-href="#Bell-curve-principle" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>Peluruhan Gaussian menciptakan kurva berbentuk lonceng yang halus yang secara bertahap mengurangi relevansi seiring bertambahnya jarak dari titik ideal. Dinamai sesuai dengan nama matematikawan Carl Friedrich Gauss, distribusi ini sering muncul di alam dan statistik, yang menjelaskan mengapa distribusi ini terasa sangat intuitif bagi persepsi manusia.</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/gaussian-decay.png" alt="Gaussian Decay" class="doc-image" id="gaussian-decay" />
   </span> <span class="img-wrapper"> <span>Peluruhan Gaussian</span> </span></p>
<p>Grafik di atas menunjukkan bagaimana peluruhan Gaussian akan memengaruhi peringkat restoran di aplikasi pencarian seluler:</p>
<ul>
<li><p><code translate="no">origin</code> (0 km): Lokasi Anda saat ini, di mana relevansi berada pada titik maksimum (1,0).</p></li>
<li><p><code translate="no">offset</code> (±300 m): "Zona nilai sempurna" di sekitar Anda-semua restoran dalam jarak 300 meter memiliki nilai relevansi penuh (1,0), sehingga memastikan bahwa pilihan yang sangat dekat tidak akan dihukum karena perbedaan jarak yang kecil.</p></li>
<li><p><code translate="no">scale</code> (±2 km): Jarak di mana relevansi turun ke nilai pembusukan-restoran yang berjarak tepat 2 kilometer memiliki nilai relevansi yang dikurangi setengahnya (0,5).</p></li>
<li><p><code translate="no">decay</code> (0.5): Skor pada jarak skala-parameter ini pada dasarnya mengontrol seberapa cepat skor berkurang seiring dengan jarak.</p></li>
</ul>
<p>Seperti yang dapat Anda lihat dari kurva, restoran yang berjarak lebih dari 2 kilometer terus mengalami penurunan relevansi, tetapi tidak pernah mencapai nol. Bahkan restoran yang berjarak 4-5 kilometer pun tetap memiliki relevansi minimal, sehingga restoran yang sangat baik tetapi jauh masih muncul di hasil Anda (meskipun peringkatnya lebih rendah).</p>
<p>Perilaku ini meniru bagaimana orang secara alami berpikir tentang relevansi jarak-tempat yang dekat lebih disukai, tetapi kita bersedia melakukan perjalanan lebih jauh untuk pilihan yang luar biasa.</p>
<h2 id="Formula" class="common-anchor-header">Rumus<button data-href="#Formula" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>Rumus matematika untuk menghitung skor peluruhan Gaussian adalah:</p>
<p>$$ S(doc) = \exp\left( -\frac{\left( \max\left(0, \left|fieldvalue_{doc} - origin\right| - offset \right) \right) \right) ^2}{2\sigma^2} \right) $$</p>
<p>Di mana:</p>
<p>$$ \sigma^2 = -\frac{scale^2}{2 \cdot \ln(peluruhan)} $$</p>
<p>Menjabarkannya dalam bahasa yang sederhana:</p>
<ol>
<li><p>Hitung seberapa jauh nilai bidang dari nilai asal: $|nilai_bidang_{doc} - asal|$</p></li>
<li><p>Kurangi offset (jika ada) tapi jangan sampai di bawah nol: $\max(0, jarak - offset)$</p></li>
<li><p>Kuadratkan jarak yang telah disesuaikan ini: $(jarak_yang_disesuaikan)^2$</p></li>
<li><p>Bagilah dengan $\sigma^2$, yang dihitung dari parameter skala dan peluruhan Anda</p></li>
<li><p>Ambil eksponen negatif, yang memberi Anda nilai antara 0 dan 1: $\exp(-value)$</p></li>
</ol>
<p>Perhitungan $\sigma^2$ mengubah skala dan parameter peluruhan Anda menjadi deviasi standar kuadrat untuk distribusi Gaussian. Inilah yang memberikan bentuk lonceng yang khas pada fungsi ini.</p>
<h2 id="Use-Gaussian-decay" class="common-anchor-header">Gunakan peluruhan Gaussian<button data-href="#Use-Gaussian-decay" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>Peluruhan Gaussian dapat diterapkan pada pencarian vektor standar dan operasi pencarian hibrida di Milvus. Di bawah ini adalah cuplikan kode kunci untuk mengimplementasikan fitur ini.</p>
<div class="alert note">
<p>Sebelum menggunakan fungsi peluruhan, Anda harus terlebih dahulu membuat koleksi dengan bidang numerik yang sesuai (seperti stempel waktu, jarak, dll.) yang akan digunakan untuk perhitungan peluruhan. Untuk contoh kerja lengkap termasuk penyiapan koleksi, definisi skema, dan penyisipan data, lihat <a href="/docs/id/tutorial-implement-a-time-based-ranking-in-milvus.md">Tutorial: Menerapkan Pemeringkatan Berbasis Waktu di Milvus</a>.</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">Membuat pemeringkat peluruhan</h3><p>Setelah koleksi Anda disiapkan dengan bidang numerik (dalam contoh ini, <code translate="no">distance</code> dalam meter dari pengguna), buat pemeringkat peluruhan Gaussian:</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> Function, FunctionType

<span class="hljs-comment"># Create a Gaussian decay ranker for location-based restaurant search</span>
ranker = Function(
    name=<span class="hljs-string">&quot;restaurant_distance_decay&quot;</span>,     <span class="hljs-comment"># Function identifier</span>
    input_field_names=[<span class="hljs-string">&quot;distance&quot;</span>],       <span class="hljs-comment"># Numeric field for distance in meters</span>
    function_type=FunctionType.RERANK,    <span class="hljs-comment"># Function type. Must be RERANK</span>
    params={
        <span class="hljs-string">&quot;reranker&quot;</span>: <span class="hljs-string">&quot;decay&quot;</span>,              <span class="hljs-comment"># Specify decay reranker</span>
        <span class="hljs-string">&quot;function&quot;</span>: <span class="hljs-string">&quot;gauss&quot;</span>,              <span class="hljs-comment"># Choose Gaussian decay</span>
        <span class="hljs-string">&quot;origin&quot;</span>: <span class="hljs-number">0</span>,                      <span class="hljs-comment"># Your current location (0 meters)</span>
        <span class="hljs-string">&quot;offset&quot;</span>: <span class="hljs-number">300</span>,                    <span class="hljs-comment"># 300m no-decay zone</span>
        <span class="hljs-string">&quot;decay&quot;</span>: <span class="hljs-number">0.5</span>,                     <span class="hljs-comment"># Half score at scale distance</span>
        <span class="hljs-string">&quot;scale&quot;</span>: <span class="hljs-number">2000</span>                     <span class="hljs-comment"># 2 km scale (2000 meters)</span>
    }
)
<button class="copy-code-btn"></button></code></pre>
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">Terapkan ke pencarian vektor standar</h3><p>Setelah menentukan pemeringkat peluruhan, Anda dapat menerapkannya selama operasi pencarian dengan meneruskannya ke parameter <code translate="no">ranker</code>:</p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Apply decay ranker to restaurant vector search</span>
result = milvus_client.search(
    collection_name,
    data=[<span class="hljs-string">&quot;italian restaurants&quot;</span>],         <span class="hljs-comment"># Query text</span>
    anns_field=<span class="hljs-string">&quot;dense&quot;</span>,                   <span class="hljs-comment"># Vector field to search</span>
    limit=<span class="hljs-number">10</span>,                             <span class="hljs-comment"># Number of results</span>
    output_fields=[<span class="hljs-string">&quot;name&quot;</span>, <span class="hljs-string">&quot;cuisine&quot;</span>, <span class="hljs-string">&quot;distance&quot;</span>],  <span class="hljs-comment"># Fields to return</span>
    ranker=ranker,                        <span class="hljs-comment"># Apply the decay ranker</span>
    consistency_level=<span class="hljs-string">&quot;Strong&quot;</span>
)
<button class="copy-code-btn"></button></code></pre>
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">Terapkan ke pencarian hibrida</h3><p>Pemeringkat peluruhan juga dapat diterapkan pada operasi pencarian hibrida yang menggabungkan beberapa bidang vektor:</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> AnnSearchRequest

<span class="hljs-comment"># Define dense vector search request</span>
dense = AnnSearchRequest(
    data=[<span class="hljs-string">&quot;italian restaurants&quot;</span>],
    anns_field=<span class="hljs-string">&quot;dense&quot;</span>,
    param={},
    limit=<span class="hljs-number">10</span>
)

<span class="hljs-comment"># Define sparse vector search request</span>
sparse = AnnSearchRequest(
    data=[<span class="hljs-string">&quot;italian restaurants&quot;</span>],
    anns_field=<span class="hljs-string">&quot;sparse_vector&quot;</span>,
    param={},
    limit=<span class="hljs-number">10</span>
)

<span class="hljs-comment"># Apply decay ranker to restaurant hybrid search</span>
hybrid_results = milvus_client.hybrid_search(
    collection_name,
    [dense, sparse],                      <span class="hljs-comment"># Multiple search requests</span>
    ranker=ranker,                        <span class="hljs-comment"># Same decay ranker</span>
    limit=<span class="hljs-number">10</span>,
    output_fields=[<span class="hljs-string">&quot;name&quot;</span>, <span class="hljs-string">&quot;cuisine&quot;</span>, <span class="hljs-string">&quot;distance&quot;</span>]
)
<button class="copy-code-btn"></button></code></pre>
<p>Untuk informasi lebih lanjut tentang operasi pencarian hibrida, lihat <a href="/docs/id/multi-vector-search.md">Pencarian Hibrida Multi-Vektor</a>.</p>
